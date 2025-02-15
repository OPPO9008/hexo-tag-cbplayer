# hexo-tag-cbplayer
本项目是将[cdnbye](https://github.com/cdnbye)的CBPlayer运行在hexo的插件

可以实现p2p加速视频下载与节约流量，让访客成为你的cdn

感谢关注这个插件的人们，感谢aplayer的hexo插件作者@grzhan，感谢A or D播放器作者@Diygod

借鉴项目：https://github.com/MoePlayer/hexo-tag-dplayer

这个项目的维护者完全不会js ，是靠查谷歌解决的

所以有什么bug很长时间没解决的，自求多福吧

如果您能修复的话，也希望请您修复一下提交个pr什么的，祝君安康


---------------------------------------------



Embed CBPlayer([https://github.com/cdnbye/CBPlayer](https://github.com/DIYgod/DPlayer)) in Hexo posts/pages.

[Hexo Demo](https://galgamer.xyz/article/32619#%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9C%96)


## npm install

	npm install hexo-tag-cbplayer --save

## Usage

	{% cbplayer key=value ... %}

key can be 

    dplayer options:
        'autoplay', 'loop', 'screenshot', 'hotkey', 'mutex', 'dmunlimited' : bool options, use "yes" "y" "true" "1" "on" or just without value to enable
        'preload', 'theme', 'lang', 'logo', 'url', 'pic', 'thumbnails', 'vidtype', 'suburl', 'subtype', 'subbottom', 'subcolor', 'subcolor', 'id', 'api', 'token', 'addition', 'dmuser' : string arguments
        'volume', 'maximum' : number arguments
    container options:
        'width', 'height' : string, used in container element style
    other:
        'code' : value of this key will be append to script tag

arguments to CBPlayer options mapping:

    {
        container: "you needn't set this",
        autoplay: 'autoplay',
        theme: 'theme',
        loop: 'loop',
        lang: 'lang',
        screenshot: 'screenshot',
        hotkey: 'hotkey',
        preload: 'preload',
        logo: 'logo',
        volume: 'volume',
        mutex: 'mutex',
        video: {
            url: 'url',
            pic: 'pic',
            thumbnails: 'thumbnails',
            type: 'vidtype',
        },
        subtitle: {
            url: 'suburl',
            type: 'subtype',
            fontSize: 'subsize',
            bottom: 'subbottom',
            color: 'subcolor',
        },
        danmaku: {
            id: 'id',
            api: 'api',
            token: 'token',
            maximum: 'maximum',
            addition: ['addition'],
            user: 'dmuser',
            unlimited: 'dmunlimited',
        },
        icons: 'icons',
        contextmenu: 'menu',
    }
    
see dplayer documents for more infomation.

for example:

    {% cbplayer "url=https://moeplayer.b0.upaiyun.com/dplayer/hikarunara.mp4" "addition=https://dplayer.daoapp.io/bilibili?aid=4157142" "api=https://api.prprpr.me/dplayer/" "pic=https://moeplayer.b0.upaiyun.com/dplayer/hikarunara.jpg" "id=9E2E3368B56CDBB4" "loop=yes" "theme=#FADFA3" "autoplay=false" "token=tokendemo" %}
    {% cbplayer 'url=some.mp4' "id=someid" "api=https://api.prprpr.me/dplayer/" "addition=/some.json" 'code=player.on("loadstart",function(){console.log("loadstart")})' "autoplay" %} 


## PJAX compatible

```js
$(document).on('pjax:start', function () {
    if (window.dplayers) {
        for (let i = 0; i < window.dplayers.length; i++) {
            window.dplayers[i].destroy();
        }
        window.dplayers = [];
    }
});
```

## Customization

You can modify variables `scriptDir`(default: "/assets/js/" ) and `styleDir`(default: "/assets/css/") in `index.js` according to your blog's directory structure.

or just use _config.yml configuration:

    # on _config.yml of hexo-site
    hexo-tag-dplayer:
      js_path: /path/to/your/default/path
      css_path: /sth
      default: #default tag argument 
        id: somedefid # equals to setting id=somedefid in all {%dplayer%} tags
        api: https://api.prprpr.me/dplayer/
        #and other options...

## Issue

If any issue occurs, tell me via issue, use a hexo raw tag like below to use dplayer:

    {% raw %}
    <div id="player1" class="dplayer"></div>
    <script src="dist/DPlayer.min.js"></script><!-- use your path -->
    <script>
    var dp = new DPlayer({{
        container: document.getElementById('dplayer'),
        autoplay: false,
        theme: '#FADFA3',
        loop: true,
        screenshot: true,
        hotkey: true,
        logo: 'logo.png',
        volume: 0.2,
        mutex: true,
        video: {
            url: 'demo.mp4',
            pic: 'demo.png',
            thumbnails: 'thumbnails.jpg',
            type: 'auto'
        },
        subtitle: {
            url: 'webvtt.vtt',
            type: 'webvtt',
            fontSize: '25px',
            bottom: '10%',
            color: '#b7daff'
        },
        danmaku: {
            id: 'demo',
            api: 'https://api.prprpr.me/dplayer/',
            token: 'demo',
            maximum: 3000,
            user: 'DIYgod',
            margin: {
                bottom: '15%'
            },
            unlimited: true
        },
        contextmenu: [
            {
                text: 'custom contextmenu',
                link: 'https://github.com/MoePlayer/DPlayer'
            }
        ]
    });
    </script>
    {% endraw %}
    
see [DPlayer](https://github.com/DIYgod/DPlayer) for usage detail

## Todo

- [x] Publish it to the [hexo plugin list](https://hexo.io/plugins) and npm

## LICENSE

MIT
