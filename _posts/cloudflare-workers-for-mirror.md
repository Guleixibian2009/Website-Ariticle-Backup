---
title: 临时解决方案：Cloudflare Workers与镜像站
date: 2022-09-17 21:49:30
tags:
- Cloudflare
- 加速
categories:
- 加速
---

最早接触到`Cloudflare`是在研究`jsdelivr`被墙后的解决方案，发现一个`cloudflare.jsdelivr.net`的节点。那是我第一次听到`Cloudflare`的大名。可没想到，真正把我拉回`Cloudflare`的，不是所谓高防`DDOS`，也不是`CDN`加速，竟梅开二度又是被墙。这次，是`Cloudflare`自己被墙了。

<!--more-->

引用另一篇文章（`Hexo`网站教程）：

> **《论我捣鼓`GiTalk`的简要过程》**
> 
> 写到这里我本想去截图，结果一看启动不起来，没办法新建`issue`也没法登录`GitHub`账号。在排查了设置、网络的问题后，我发现有个致命的问题：`cors-anywhere.azm.workers.dev`被墙掉，然后`GiTalk`无法进行`GitHub oauth`，就不能用了。
> 
> 我于是尝试自己搭`worker`，结果发现是所有`Cloudflare worker`的链接都被墙掉了，然后我就彻底没招了，就只好作罢。不过......真的吗？
> 
> 后来我找到了`GiTalk`的仓库，里面有类似的`Issue`，甚至翻出了`CORS Anywhere`的仓库，找到了一个基于`Heroku`的备用`demo`链接。在一个`Issue`的[某条评论](https://github.com/Rob--W/cors-anywhere/issues/301#issuecomment-870990778)、[某条评论](https://github.com/Rob--W/cors-anywhere/issues/301#issuecomment-1012060775)中找到了一些备用链接。于是，就可以恢复正常了！
> 
> **另及：今年（2022）11月28号`Heroku`会关闭所有的免费服务，所以你看到类似`herokuapp.com`的链接都不用试了...**

这个`cors-anywhere.azm.workers.dev`，就是基于`Cloudflare Workers`的。上文也提到了我自己搭`Workers`，在这其中也有一点意外地收获。

## 1. 关于我们今天到底在干什么

`Cloudflare Workers`，乍一听，我也没猜出这是什么东西。其实`Workers`是`Cloudflare`提供的免费服务器，类似`GitHub`给你一个二级域名（`GitHub`就是`github.io`，`Cloudflare Workers`是`workers.dev`）。这个`CF Workers`是支持自定义处理逻辑，说白点自己用`JavaScript`写脚本。当然我不会把事情变得太复杂，肯定是有可重用的模板的。

但是我们没事儿搭服务器干嘛？不知道各位有没有听说过反向代理这回事。差不多如此：

```sequence
Client --> BlockedServer: GET xxx
note left of Client: I cannot GET!
Client -> CF Worker: GET Blocked Server for me!
note right of CF Worker: I can GET!
CF Worker -> BlockedServer: GET xxx
BlockedServer -> CF Worker: Responce xxx
CF Worker -> Client: Responce xxx
```

![](https://s1.ax1x.com/2022/09/19/x9oTDU.png)

~~其实说白了这也是一种fq的方式嘛。~~

## 2. 关于你的`Cloudflare`账号

照例的话，我们肯定是要简要说一下官网和账号的....<https://www.cloudflare.com/>，很人性化的就跳到中文版啊。

![](https://s1.ax1x.com/2022/09/19/x9oL59.png)

然后点击注册就好了耶：

![](https://s1.ax1x.com/2022/09/19/x9o7bF.png)

然后有一些配置，按照自己的喜好填就好了啊。不过由于资金问题和一些使用方式上的原因，我们选`Free Plan`就可以了，千万不要为了这个白买高级版，每天100000个请求完全完全够用了！

## 3. 开始搭建`Worker`

### 3.1 初始化`Worker`

我们接下来以访问速度慢的`GitHub`和无法访问的`Google`为例。

![](https://s1.ax1x.com/2022/09/19/x9obE4.png)

我们在左侧的菜单中找到`Workers`，然后新建服务：

![](https://s1.ax1x.com/2022/09/19/x9oXCR.png)

由于我们只需要一个`worker`就可以完成一切任务，我就没有新注册了。

![](https://s1.ax1x.com/2022/09/19/x9oqUJ.png)

进来之后有这样一个界面：

![](https://s1.ax1x.com/2022/09/24/xAMkng.png)

我们点击快速编辑，进入编辑页面：

![](https://s1.ax1x.com/2022/09/24/xAME7j.png)

左边是处理逻辑，右边则是预览部分。

### 3.2 加入代码

先复制一下下面这段代码：

```js
// 你要镜像的网站.
const upstream = 'www.google.com'

// 镜像网站的目录，比如你想镜像某个网站的二级目录则填写二级目录的目录名，镜像 google 用不到，默认即可.
const upstream_path = '/'

// 镜像站是否有手机访问专用网址，没有则填一样的.
const upstream_mobile = 'www.google.com'

// 屏蔽国家和地区.
const blocked_region = ['KP', 'SY', 'PK', 'CU']

// 屏蔽 IP 地址.
const blocked_ip_address = ['0.0.0.0', '127.0.0.1']

// 镜像站是否开启 HTTPS.
const https = true

// 文本替换.
const replace_dict = {
    '$upstream': '$custom_domain',
    '//www.google.com': ''
}

// 以下保持默认，不要动
addEventListener('fetch', event => {
    event.respondWith(fetchAndApply(event.request));
})

async function fetchAndApply(request) {

    const region = request.headers.get('cf-ipcountry').toUpperCase();
    const ip_address = request.headers.get('cf-connecting-ip');
    const user_agent = request.headers.get('user-agent');

    let response = null;
    let url = new URL(request.url);
    let url_hostname = url.hostname;

    if (https == true) {
        url.protocol = 'https:';
    } else {
        url.protocol = 'http:';
    }

    if (await device_status(user_agent)) {
        var upstream_domain = upstream;
    } else {
        var upstream_domain = upstream_mobile;
    }

    url.host = upstream_domain;
    if (url.pathname == '/') {
        url.pathname = upstream_path;
    } else {
        url.pathname = upstream_path + url.pathname;
    }

    if (blocked_region.includes(region)) {
        response = new Response('Access denied: WorkersProxy is not available in your region yet.', {
            status: 403
        });
    } else if (blocked_ip_address.includes(ip_address)) {
        response = new Response('Access denied: Your IP address is blocked by WorkersProxy.', {
            status: 403
        });
    } else {
        let method = request.method;
        let request_headers = request.headers;
        let new_request_headers = new Headers(request_headers);

        new_request_headers.set('Host', url.hostname);
        new_request_headers.set('Referer', url.hostname);

        let original_response = await fetch(url.href, {
            method: method,
            headers: new_request_headers
        })

        let original_response_clone = original_response.clone();
        let original_text = null;
        let response_headers = original_response.headers;
        let new_response_headers = new Headers(response_headers);
        let status = original_response.status;

        new_response_headers.set('access-control-allow-origin', '*');
        new_response_headers.set('access-control-allow-credentials', true);
        new_response_headers.delete('content-security-policy');
        new_response_headers.delete('content-security-policy-report-only');
        new_response_headers.delete('clear-site-data');

        const content_type = new_response_headers.get('content-type');
        if (content_type.includes('text/html') && content_type.includes('UTF-8')) {
            original_text = await replace_response_text(original_response_clone, upstream_domain, url_hostname);
        } else {
            original_text = original_response_clone.body
        }

        response = new Response(original_text, {
            status,
            headers: new_response_headers
        })
    }
    return response;
}

async function replace_response_text(response, upstream_domain, host_name) {
    let text = await response.text()

    var i, j;
    for (i in replace_dict) {
        j = replace_dict[i]
        if (i == '$upstream') {
            i = upstream_domain
        } else if (i == '$custom_domain') {
            i = host_name
        }

        if (j == '$upstream') {
            j = upstream_domain
        } else if (j == '$custom_domain') {
            j = host_name
        }

        let re = new RegExp(i, 'g')
        text = text.replace(re, j);
    }
    return text;
}


async function device_status(user_agent_info) {
    var agents = ["Android", "iPhone", "SymbianOS", "Windows Phone", "iPad", "iPod"];
    var flag = true;
    for (var v = 0; v < agents.length; v++) {
        if (user_agent_info.indexOf(agents[v]) > 0) {
            flag = false;
            break;
        }
    }
    return flag;
}
```

然后我们把它复制到左边的代码块中。这里面有几个我们需要修改的地方：

```js
// 你要镜像的网站.
const upstream = 'www.google.com'

// 镜像网站的目录，比如你想镜像某个网站的二级目录则填写二级目录的目录名，镜像 google 用不到，默认即可.
const upstream_path = '/'

// 镜像站是否有手机访问专用网址，没有则填一样的.
const upstream_mobile = 'www.google.com'

// 文本替换.
const replace_dict = {
    '$upstream': '$custom_domain',
    '//www.google.com': ''
}
```

一定要保证`upstream`、`upstream_mobile`、`replace_dict`中三个网址是一样的。

然后保存一下，点保存并部署即可。

现在看一下效果吧：

![](https://s1.ax1x.com/2022/09/24/xAMABQ.png)

![](https://s1.ax1x.com/2022/09/24/xAMijS.png)

可惜的是，那个部署出来的`workers.dev`链接是不能使用的。不过反过来想，我们已经获得了谷歌的永久访问，不是么？

**THE END**感谢您的阅读\~
