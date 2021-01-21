## 新年快乐
**解析只对部分用户开放,本次主要更新**
```
新增 query.context,解析过程parse和query获取了同个api,可以设置query.context.key=value,减少api的重复调用
修改 -x ignore,不走系统代理
新增 extra.multi,可以单独控制该资源类型的下载线程
新增 extra.retry,segs分段解析出错时,会重新调用parse函数重新解析获取segs
修改 extra.reload逻辑,下载速度小于10k或异常退出,待下一次轮询时,会调用重载函数reload,重新获取segs切片后,继续下载.此模式适用于腾讯视频限速 
新增 解析重载函数reload,资源下载出错时,可以单独解析切片segs[idx]['url']
新增 解析备用函数afresh,parse函数解析出错时,会调用afresh函数执行另外一个方案解析
新增 -i --info参数,只输出资源信息,不下载
新增 -a --capture参数,视频截取更方便了,不需要整段下载后再去截取 -a -ts 60 -te 120
修复 YouTube sig参数缺失导致无法下载播放,暂不支持mpd
修复 YouTube添加代理后,只能下载,不能在线播放bug  
新增 YouTube itag组合播放 -itag 315:251 -p mpv
新增 --player=temp,边下边播 
新增 -f --format参数,下载完直接调用ffmpeg格式转码
修改 -u --multi参数,全局默认多线程下载,控制进程数
新增 --init 用户自定义配置,初始安装执行--init=r生成config.py,--init=b备份config.py
移除 python3.6以下版本支持
```

## 版本要求
**python>=3.6** 
## 安装文件路径查询
```
pip3 show vparse
```
## 扩展依赖

```
'requests', 'pycryptodome', 'pysocks','pyexecjs', "coloredlogs"
```
 
**部分解析运行JS,需要安装NodeJs环境.如果你的操作环境支持[quickjs](https://github.com/PetterS/quickjs),可以不用安装NodeJs**

```
pip3 install quickjs
```
## 使用说明
**默认打印JSON (Parse)**
```
$ vparse https://www.iqiyi.com/v_19rv876x9k.html
{'title': '刀剑神域 爱丽丝篇 异界战争 第5集 开战前夜', 'image': 'http://pic7.iqiyipic.com/image/20191110/ed/52/v_140769663_m_601_m1_480_270.jpg', 'vid': '1f744786c7f4b15d4ec70b08d030bbfd', 'tvid': '9177088900', 'pay': '', 'duration': 1445, 'hd': 5, 'parse': 'https://www.iqiyi.com/v_19rv876x9k.html', 'type': 'iqiyi', 'category': 'video', 'streams': {'segs': [{'url': 'http://cache.m.iqiyi.com/mus/246382101/3dfabf1047a5363e76c72e12fece8764/afbe8fd3d73448c9//20191107/00/78/ef4f5563bef229be82c368d0cb153807.m3u8', 'duration': 1445, 'size': 325434438}], 'm3u8': 'http://cache.m.iqiyi.com/mus/246382101/3dfabf1047a5363e76c72e12fece8764/afbe8fd3d73448c9//20191107/00/78/ef4f5563bef229be82c368d0cb153807.m3u8'}, 'quality': ['极速', '流畅', '高清', '720P', '1080P', '1080P50'], 'multirates': 6, 'show': '1080P', 'playback': 'm3u8', 'ext': 'm3u8'}
```
**-d --download : 下载 (Download)** 
```
$ vparse https://www.iqiyi.com/v_19rv876x9k.html -d
site:                爱奇艺(AQIYI)
title:               刀剑神域 爱丽丝篇 异界战争 第5集 开战前夜
image:               http://pic7.iqiyipic.com/image/20191110/ed/52/v_140769663_m_601_m1_480_270.jpg
vid:                 1f744786c7f4b15d4ec70b08d030bbfd
tvid:                9177088900
duration:            1445
parse:               https://www.iqiyi.com/v_19rv876x9k.html
hd:                  5
stream:
    - ext:           m3u8
      quality:       ['极速', '流畅', '高清', '720P', '1080P', '1080P50']
      show:          1080P
      multirates:    6
      dir:           /Users/air/video/iqiyi

Hls: http://cache.m.iqiyi.com/mus/246382101/3dfabf1047a5363e76c72e12fece8764/afbe8fd3d73448c9//20191107/00/78/ef4f5563bef229be82c368d0cb153807.m3u8


[1 / 190] |-████████████████████████████████-|100%  2170.78kb/s 0.73M/0.85M  
```
**-f --format : 格式转换 (FFMPEG format)** 
```
$ vparse https://www.iqiyi.com/v_19rv876x9k.html -d -f flv
```
**-j --json : 打印格式化JSON (Format JSON and print)**
```
$ vparse https://www.iqiyi.com/v_19rv876x9k.html -j
{
    "duration": 1445,
    "ext": "m3u8",
    "hd": 5,
    "image": "http://pic7.iqiyipic.com/image/20191110/ed/52/v_140769663_m_601_m1_480_270.jpg",
    "multirates": 6,
    "parse": "https://www.iqiyi.com/v_19rv876x9k.html",
    "pay": "",
    "playback": "m3u8",
    "quality": [
        "极速",
        "流畅",
        "高清",
        "720P",
        "1080P",
        "1080P50"
    ],
    "show": "1080P",
    "streams": {
        "m3u8": "http://cache.m.iqiyi.com/mus/246382101/3dfabf1047a5363e76c72e12fece8764/afbe8fd3d73448c9//20191107/00/78/ef4f5563bef229be82c368d0cb153807.m3u8",
        "segs": [
            {
                "duration": 1445,
                "size": 325434438,
                "url": "http://cache.m.iqiyi.com/mus/246382101/3dfabf1047a5363e76c72e12fece8764/afbe8fd3d73448c9//20191107/00/78/ef4f5563bef229be82c368d0cb153807.m3u8"
            }
        ]
    },
    "title": "刀剑神域 爱丽丝篇 异界战争 第5集 开战前夜",
    "tvid": "9177088900",
    "type": "iqiyi",
    "vid": "1f744786c7f4b15d4ec70b08d030bbfd",
    "category": "video"
}
```
**-r --hd : 获取其他分辨率解析链接 (Video resolution selection)**

```
$ vparse https://www.iqiyi.com/v_19rv876x9k.html -j -r 1
 
{
    "duration": 1445,
    "ext": "m3u8",
    "hd": 1,
    "image": "http://pic7.iqiyipic.com/image/20191110/ed/52/v_140769663_m_601_m1_480_270.jpg",
    "multirates": 6,
    "parse": "https://www.iqiyi.com/v_19rv876x9k.html",
    "pay": "",
    "playback": "m3u8",
    "quality": [
        "极速",
        "流畅",
        "高清",
        "720P",
        "1080P",
        "1080P50"
    ],
    "show": "极速",
    "streams": {
        "m3u8": "http://cache.m.iqiyi.com/mus/246382101/e0af4c681ed3af040f893d7cb249efcf/afbe8fd3d73448c9//20191107/30/5b/433b7103cdaa1a6e542f88bc491ed6d5.m3u8",
        "segs": [
            {
                "duration": 1445,
                "size": 28441560,
                "url": "http://cache.m.iqiyi.com/mus/246382101/e0af4c681ed3af040f893d7cb249efcf/afbe8fd3d73448c9//20191107/30/5b/433b7103cdaa1a6e542f88bc491ed6d5.m3u8"
            }
        ]
    },
    "title": "刀剑神域 爱丽丝篇 异界战争 第5集 开战前夜",
    "tvid": "9177088900",
    "type": "iqiyi",
    "vid": "1f744786c7f4b15d4ec70b08d030bbfd",
    "category": "video"
}
```
**-q --query : 只获取链接信息 (Output only video information)**
```
$ vparse -q -j -t le http://www.le.com/ptv/vplay/1277141.html http://www.le.com/ptv/vplay/1277142.html
{
    "hd": 5,
    "image": "http://i3.letvimg.com/lc08_yunzhuanma/201611/16/16/33/76362b5277a31258e7bbfc4ee7066b7c_v2_MjcwMzgzNA==/thumb/2_640_320.jpg",
    "parse": "http://www.le.com/ptv/vplay/1277141.html",
    "title": "钢之炼金术师FA 第04话",
    "tvid": "1351417",
    "type": "le",
    "vid": "1277141",
    "category": "video"
}
```
**-c --cookie : cookie 支持文本或字符串 (Cookies, supports text and strings)**

```
$ vparse https://www.iqiyi.com/v_19rvasnkfk.html -c ./iqiyi.txt  
$ vparse https://www.iqiyi.com/v_19rvasnkfk.html -c "name=value; name2=value2;"  
```
**-t --type : urls为id形式时使用 (Add when urls is not a URL)**
```
$ vparse 15195741 -t bilibili 
```
**-v --category : urls为id形式时使用 (Add when urls is not a URL)**
```
$ vparse 229285 -t netease -v music
```

**-x --proxy: proxy代理 (Proxy)**

```
$ vparse https://www.youtube.com/watch?v=zBKei6Ji_WI -x socks5://127.0.0.1:1080 
```
**-y --http: http代理 (Youtube http proxy)**

```
$ vparse https://www.youtube.com/watch?v=zBKei6Ji_WI -x socks5://127.0.0.1:1080 -y http://127.0.0.1:10800
```
**-l --playlist : 列表获取 (Add when urls is playlist)**

```
$ vparse http://www.le.com/comic/45402.html -l -q -j
{
    "hd": 5,
    "image": "http://i2.letvimg.com/lc09_yunzhuanma/201611/16/11/57/5718cbc33bd8c2cd6270066c73a187ce_v2_MjcwMzgzOA==/thumb/5_640_320.jpg",
    "parse": "1277143",
    "title": "钢之炼金术师FA 第01话",
    "tvid": "1351419",
    "type": "le",
    "vid": "1277143",
    "category": "video"
}
{
    "hd": 5,
    "image": "http://i3.letvimg.com/lc08_yunzhuanma/201611/16/11/48/bc507343910aedd19c0d194e835151c9_v2_MjcwMzg0Mg==/thumb/6_640_320.jpg",
    "parse": "1277145",
    "title": "钢之炼金术师FA 第02话",
    "tvid": "1351421",
    "type": "le",
    "vid": "1277145",
    "category": "video"
}
{
    "hd": 5,
    "image": "http://i1.letvimg.com/lc12_yunzhuanma/201611/16/14/39/83093e33235cbf0cc403994073d5affa_v2_MjcwMzgzNg==/thumb/6_640_320.jpg",
    "parse": "1277142",
    "title": "钢之炼金术师FA 第03话",
    "tvid": "1351418",
    "type": "le",
    "vid": "1277142",
    "category": "video"
}
{
    "hd": 5,
    "image": "http://i3.letvimg.com/lc08_yunzhuanma/201611/16/16/33/76362b5277a31258e7bbfc4ee7066b7c_v2_MjcwMzgzNA==/thumb/2_640_320.jpg",
    "parse": "1277141",
    "title": "钢之炼金术师FA 第04话",
    "tvid": "1351417",
    "type": "le",
    "vid": "1277141",
    "category": "video"
} 
```
**-b --choose : 列表选择获取 a\[,b,c...\] 或 a:b (If the urls is a playlist)**
```
$ vparse http://www.le.com/comic/45402.html -l -q -j -o 12,26,55
{
    "hd": 5,
    "image": "http://i0.letvimg.com/lc08_yunzhuanma/201611/16/14/49/e6155d820bde52b4b88bf5c4c66851ef_v2_MjcwMzg1Ng==/thumb/2_640_320.jpg",
    "parse": "1277152",
    "title": "钢之炼金术师FA 第12话",
    "tvid": "1351428",
    "type": "le",
    "vid": "1277152",
    "category": "video"
}
{
    "hd": 5,
    "image": "http://i3.letvimg.com/lc13_yunzhuanma/201611/16/15/02/8115319d2a0d790a32cc759780818471_v2_MjcwMzg4NA==/thumb/2_640_320.jpg",
    "parse": "1277166",
    "title": "钢之炼金术师FA 第26话",
    "tvid": "1351442",
    "type": "le",
    "vid": "1277166",
    "category": "video"
}
{
    "hd": 5,
    "image": "http://i2.letvimg.com/lc13_yunzhuanma/201611/16/15/47/9aec8f9f7e50d11bbda8cf20b4ba655b_v2_MjcwMzk1OA==/thumb/2_640_320.jpg",
    "parse": "1277203",
    "title": "钢之炼金术师FA 第55话",
    "tvid": "1351479",
    "type": "le",
    "vid": "1277203",
    "category": "video"
}
```  
**-o --language : 语言选项 (Select language options)**
```
$ vparse https://v.youku.com/v_show/id_XMzQ3OTU4NjA3Ng==.html -j -o yue
{
    "duration": 6122.33,
    "ext": "mp4",
    "hd": 4,
    "image": "https://vthumb.ykimg.com/054101015D847F898B6C069AAD259696",
    "multirates": 4,
    "parse": "https://v.youku.com/v_show/id_XMzQ3OTU4NjA3Ng==.html",
    "pay": 1,
    "playback": "m3u8",
    "quality": [
        "mp4sd",
        "mp4hd",
        "mp4hd2v2",
        "mp4hd3v2"
    ],
    "show": "mp4hd3v2",
    "streams": {
        "extra": {
            "language": [
                {
                    "langcode": "guoyu",
                    "language": "普通话",
                    "url": "https://v.youku.com/v_show/id_XMzQ3OTU4NjA3Ng==.html"
                },
                {
                    "langcode": "yue",
                    "language": "粤语",
                    "url": "https://v.youku.com/v_show/id_XMzU5NzIxNzg3Mg==.html"
                }
            ]
        },
        "m3u8": "http://pl-ali.youku.com/playlist/m3u8?vid=XMzU5NzIxNzg3Mg%3D%3D&type=mp4hd3v3",
        "segs": [
            {
                "duration": 135.083,
                "url": "http://vali.cp31.ott.cibntv.net/697674F07A333714DB2726E1E/03000C2D005CDEA5757D338055EEB34AD3A715-479C-4458-BCBB-9A88B064C876.mp4?ccode=0511&duration=135"
            },
        ]
    },
    "title": "唐伯虎点秋香[粤语]",
    "type": "youku",
    "vid": "XMzQ3OTU4NjA3Ng==",
    "category": "video"
}
```
**-p --player : 播放器播放 (Directly play the video with PLAYER like mpv)**

```
$ vparse https://www.iqiyi.com/v_19rv876x9k.html -p mpv

site:                爱奇艺(AQIYI)
title:               刀剑神域 爱丽丝篇 异界战争 第5集 开战前夜
image:               http://pic7.iqiyipic.com/image/20191110/ed/52/v_140769663_m_601_m1_480_270.jpg
vid:                 1f744786c7f4b15d4ec70b08d030bbfd
tvid:                9177088900
duration:            1445
parse:               https://www.iqiyi.com/v_19rv876x9k.html
hd:                  5
stream:
    - ext:           m3u8
      quality:       ['极速', '流畅', '高清', '720P', '1080P', '1080P50']
      show:          1080P
      multirates:    6


Playing: http://cache.m.iqiyi.com/mus/246382101/3dfabf1047a5363e76c72e12fece8764/afbe8fd3d73448c9//20191107/00/78/ef4f5563bef229be82c368d0cb153807.m3u8
```
**-n --name : 自定义下载文件名 (Video downloaded with the file name you want)**
```
$ vparse http://www.le.com/ptv/vplay/1277141.html -n 乐视视频标题测试 -d
site:                乐视(LE)
title:               乐视视频标题测试
vid:                 1277141
duration:            1469
parse:               http://www.le.com/ptv/vplay/1277141.html
hd:                  2
stream:
    - ext:           m3u8
      quality:       ['流畅', '标清']
      show:          标清
      multirates:    2
      dir:           /Users/air/Desktop/video/le

Hls: http://play.g3proxy.lecloud.com//vod/v2/MjMyLzUzLzIzL2xldHYtdXRzLzE0L3Zlcl8wMF8yMi0xMDcyODU0Njk0LWF2Yy0zODk4MTctYWFjLTMyMDAwLTE0Njk1NTMtNzkwNjcyMzAtNzBlMWUyODg5ODBiMTkwNmZlODI1M2JkMTYzMjc5ZDItMTQ3OTI4NTc2MjgwOS5tcDQ=?b=430&mmsid=1351417&tm=1574761118


[1 / 86] |-████████████████████████████████-|100%  3998.67kb/s 0.00M/0.18M 
```
**-s --debug : 调试 (Debug)**

```
$ vparse -s https://www.bilibili.com/video/av9196627/
DEBUG:common.py:324:requests:get
url: https://www.bilibili.com/video/av9196627/
useragent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.13; rv:67.0) Gecko/20100101 Firefox/67.0
----------------------------------------------------
DEBUG:common.py:324:requests:get
url: http://api.bilibili.com/view?appkey=12737ff7776f1ade&batch=1&page=1&id=9196627
useragent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.13; rv:67.0) Gecko/20100101 Firefox/67.0
----------------------------------------------------
DEBUG:bilibili.py:88:query:getInfo: {"tid":24,"typename":"MAD\u00b7AMV","arctype":"Original","play":104418,"review":433,"video_review":615,"favorites":10237,"title":"\u3010\u8865\u5e27\u5411\/AMV\u3011\u4e00\u82b1\u4e00\u8349\u4e00\u4e16\u754c","allow_bp":0,"allow_feed":0,"allow_download":1,"description":"\u2018\u82b1\u2019\uff0c\u70df\u82b1\uff0c\u96e8\u82b1\uff0c\u96ea\u82b1\u7b49\u4e00\u5207\u4e16\u95f4\u7f8e\u4e3d\u4e4b\u7269\uff0c\u2018\u8349\u2019\uff0c\u4e00\u98a6\u4e00\u7b11\uff0c\u4e00\u66f2\u4e00\u8c03\uff0c\u4e00\u5207\u5bcc\u6709\u84ec\u52c3\u751f\u6c14\u4e4b\u7269\u3002\u8fd9\u662f\u6807\u9898\u2018\u4e16\u754c\u2019\u7684\u6700\u540e\u4e00\u4f5c\u4e86\uff0c\u4f5c\u54c1\u4e2d\u7684\u8865\u5e27\u624b\u6cd5\u5927\u591a\u4e3a\u5e38\u901f\u8865\u5e27\u800c\u975e\u5feb\u6162\u7f13\u52a8\uff0c\u6bd4\u8d77\u524d\u9762\u4e24\u4e2a\u4f5c\u54c1\u6709\u4e9b\u8d8b\u4e8e\u5e73\u6de1\uff0c\u5e0c\u671b\u8ba9\u5185\u5fc3\u5e73\u9759\u4e0b\u6765\uff0c\u611f\u53d7\u4e16\u95f4\u7684\u7f8e\u597d\u3002\nBGM:onoken - byebye\n\u5c01\u9762P\u7ad9ID=61823065","tag":null,"pic":"https:\/\/i0.hdslb.com\/bfs\/archive\/f2b6833f8d732c6b624e11572b9b86afac7d9687.jpg","author":"JF\u00b7\u4e0b\u5f26","mid":1300401,"face":"https:\/\/i1.hdslb.com\/bfs\/face\/90632f0f94136b0b132a79c09b8e881db0f9c25d.jpg","pages":1,"instant_server":"chat.bilibili.com","created":1489650761,"created_at":"2017-03-16 15:52","credit":"--","coins":6868,"spid":null,"src":"c","cid":15195741,"partname":"\u6700\u7ec8_x264","part":"\u6700\u7ec8_x264","from":"vupload","type":"vupload","vid":"vupload_15195741","offsite":"https:\/\/share.b23.tv\/flash.swf?aid=9196627&page=1","list":[{"page":1,"type":"vupload","part":"\u6700\u7ec8_x264","cid":15195741,"weblink":"","vid":"","has_alias":false}]} 

----------------------------------------------------
DEBUG:extractor.py:195:root:query: {"vid": 15195741, "image": "https://i0.hdslb.com/bfs/archive/f2b6833f8d732c6b624e11572b9b86afac7d9687.jpg", "tvid": "9196627", "page": 1, "title": "【补帧向/AMV】一花一草一世界", "hd": 6, "parse": "https://www.bilibili.com/video/av9196627/", "type": "bilibili", "category": "video"}
----------------------------------------------------
DEBUG:common.py:324:requests:get
url: https://app.bilibili.com/v2/playurl?appkey=iVGUTjsxvpLeuDCf&build=4140&buvid=ef5efdc0452641eb235cd424dfa03660&cid=15195741&device=phone&otype=json&platform=html5&qn=80&type=mp4&sign=d6f949304746364a1f53fdedf68d676a
useragent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.13; rv:67.0) Gecko/20100101 Firefox/67.0
----------------------------------------------------
DEBUG:bilibili.py:174:parse:mSource: {"from":"local","result":"suee","quality":48,"format":"hdmp4","timelength":128021,"accept_format":"hdmp4,mp4,mp4","accept_description":["高清 720P","流畅 360P","极速 240P"],"accept_quality":[48,16,6],"video_codecid":7,"video_project":true,"seek_param":"start","seek_type":"second","durl":[{"order":1,"length":128021,"size":20025602,"url":"http://upos-sz-mirrorkodo.bilivideo.com/upgcxcode/41/57/15195741/15195741-1-48.mp4?e=ig8euxZM2rNcNbhHhwdVhoMznWdVhwdEto8g5X10ugNcXBB_&deadline=1609912483&gen=playurl&nbs=1&oi=2016110196&os=kodobv&platform=html5&trid=852fdc2d54f84209b0cdd83cf030c3f1&uipk=5&upsig=9eb4781a50ec1f88d6df31fc92b34f99&uparams=e,deadline,gen,nbs,oi,os,platform,trid,uipk&mid=0"}]} 

----------------------------------------------------
DEBUG:common.py:324:requests:get
url: https://interface.bilibili.com/v2/playurl?appkey=iVGUTjsxvpLeuDCf&build=4140&buvid=ef5efdc0452641eb235cd424dfa03660&cid=15195741&device=phone&otype=json&platform=html5&qn=80&quality=80&type=flv&sign=b03263f612a951ee889b5e0d0f472ca7
useragent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.13; rv:67.0) Gecko/20100101 Firefox/67.0
----------------------------------------------------
DEBUG:common.py:324:requests:get
url: https://interface.bilibili.com/v2/playurl?appkey=iVGUTjsxvpLeuDCf&build=4140&buvid=ef5efdc0452641eb235cd424dfa03660&cid=15195741&device=phone&otype=json&platform=html5&qn=74&quality=74&type=flv&sign=3a203730759d96ecc02f62e95cd52b74
useragent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.13; rv:67.0) Gecko/20100101 Firefox/67.0
----------------------------------------------------
DEBUG:bilibili.py:230:parse:getFlvSource: {"from":"local","result":"suee","quality":64,"format":"flv720","timelength":128143,"accept_format":"flv720_p60,flv,flv720,flv480,flv360","accept_description":["高清 720P60","高清 1080P","高清 720P","清晰 480P","流畅 360P"],"accept_quality":[74,80,64,32,16],"video_codecid":7,"video_project":true,"seek_param":"start","seek_type":"offset","durl":[{"order":1,"length":128143,"size":26408334,"url":"http://upos-sz-mirrorcos.bilivideo.com/upgcxcode/41/57/15195741/15195741_da3-1-64.flv?e=ig8euxZM2rNcNbU17WdVhoMBhWUVhwdEto8g5X10ugNcXBB_&deadline=1609912484&gen=playurl&nbs=1&oi=2016110196&os=cosbv&platform=html5&trid=b76fb4872a4246b9ac126adb98613cb9&uipk=5&upsig=cc43a5e771875765482c8bceab39a65c&uparams=e,deadline,gen,nbs,oi,os,platform,trid,uipk&mid=0"}]} 

----------------------------------------------------
{'vid': 15195741, 'image': 'https://i0.hdslb.com/bfs/archive/f2b6833f8d732c6b624e11572b9b86afac7d9687.jpg', 'tvid': '9196627', 'page': 1, 'title': '【补帧向 AMV】一花一草一世界', 'hd': 4, 'parse': 'https://www.bilibili.com/video/av9196627/', 'type': 'bilibili', 'category': 'video', 'streams': {'flv': 'http://upos-sz-mirrorcos.bilivideo.com/upgcxcode/41/57/15195741/15195741_da3-1-64.flv?e=ig8euxZM2rNcNbU17WdVhoMBhWUVhwdEto8g5X10ugNcXBB_&deadline=1609912484&gen=playurl&nbs=1&oi=2016110196&os=cosbv&platform=html5&trid=b76fb4872a4246b9ac126adb98613cb9&uipk=5&upsig=cc43a5e771875765482c8bceab39a65c&uparams=e,deadline,gen,nbs,oi,os,platform,trid,uipk&mid=0', 'segs': [{'url': 'http://upos-sz-mirrorcos.bilivideo.com/upgcxcode/41/57/15195741/15195741_da3-1-64.flv?e=ig8euxZM2rNcNbU17WdVhoMBhWUVhwdEto8g5X10ugNcXBB_&deadline=1609912484&gen=playurl&nbs=1&oi=2016110196&os=cosbv&platform=html5&trid=b76fb4872a4246b9ac126adb98613cb9&uipk=5&upsig=cc43a5e771875765482c8bceab39a65c&uparams=e,deadline,gen,nbs,oi,os,platform,trid,uipk&mid=0', 'duration': 128.143, 'size': 26408334}], 'mp4': 'http://upos-sz-mirrorkodo.bilivideo.com/upgcxcode/41/57/15195741/15195741-1-48.mp4?e=ig8euxZM2rNcNbhHhwdVhoMznWdVhwdEto8g5X10ugNcXBB_&deadline=1609912483&gen=playurl&nbs=1&oi=2016110196&os=kodobv&platform=html5&trid=852fdc2d54f84209b0cdd83cf030c3f1&uipk=5&upsig=9eb4781a50ec1f88d6df31fc92b34f99&uparams=e,deadline,gen,nbs,oi,os,platform,trid,uipk&mid=0'}, 'playback': 'mp4', 'extra': {'header': {'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10.13; rv:71.0) Gecko/20100101 Firefox/71.0', 'Referer': 'https://www.bilibili.com/video/'}, 'playback': 'flv', 'headers': {'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10.13; rv:68.0) Gecko/20100101 Firefox/68.0'}}, 'otype': 'video', 'quality': ['流畅 360P', '清晰 480P', '高清 720P', '高清 1080P'], 'multirates': 4, 'ext': 'flv', 'duration': 128.143, 'show': '高清 1080P', 'site': '哔哩哔哩(BILIBILI)', 'size': 26408334}
MAC:~ air$ vparse -s https://www.bilibili.com/video/av9196627/ -j
DEBUG:common.py:324:requests:get
url: https://www.bilibili.com/video/av9196627/
useragent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.13; rv:67.0) Gecko/20100101 Firefox/67.0
----------------------------------------------------
DEBUG:common.py:324:requests:get
url: http://api.bilibili.com/view?appkey=12737ff7776f1ade&batch=1&page=1&id=9196627
useragent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.13; rv:67.0) Gecko/20100101 Firefox/67.0
----------------------------------------------------
DEBUG:bilibili.py:88:query:getInfo: {"tid":24,"typename":"MAD\u00b7AMV","arctype":"Original","play":104418,"review":433,"video_review":615,"favorites":10237,"title":"\u3010\u8865\u5e27\u5411\/AMV\u3011\u4e00\u82b1\u4e00\u8349\u4e00\u4e16\u754c","allow_bp":0,"allow_feed":0,"allow_download":1,"description":"\u2018\u82b1\u2019\uff0c\u70df\u82b1\uff0c\u96e8\u82b1\uff0c\u96ea\u82b1\u7b49\u4e00\u5207\u4e16\u95f4\u7f8e\u4e3d\u4e4b\u7269\uff0c\u2018\u8349\u2019\uff0c\u4e00\u98a6\u4e00\u7b11\uff0c\u4e00\u66f2\u4e00\u8c03\uff0c\u4e00\u5207\u5bcc\u6709\u84ec\u52c3\u751f\u6c14\u4e4b\u7269\u3002\u8fd9\u662f\u6807\u9898\u2018\u4e16\u754c\u2019\u7684\u6700\u540e\u4e00\u4f5c\u4e86\uff0c\u4f5c\u54c1\u4e2d\u7684\u8865\u5e27\u624b\u6cd5\u5927\u591a\u4e3a\u5e38\u901f\u8865\u5e27\u800c\u975e\u5feb\u6162\u7f13\u52a8\uff0c\u6bd4\u8d77\u524d\u9762\u4e24\u4e2a\u4f5c\u54c1\u6709\u4e9b\u8d8b\u4e8e\u5e73\u6de1\uff0c\u5e0c\u671b\u8ba9\u5185\u5fc3\u5e73\u9759\u4e0b\u6765\uff0c\u611f\u53d7\u4e16\u95f4\u7684\u7f8e\u597d\u3002\nBGM:onoken - byebye\n\u5c01\u9762P\u7ad9ID=61823065","tag":null,"pic":"https:\/\/i0.hdslb.com\/bfs\/archive\/f2b6833f8d732c6b624e11572b9b86afac7d9687.jpg","author":"JF\u00b7\u4e0b\u5f26","mid":1300401,"face":"https:\/\/i1.hdslb.com\/bfs\/face\/90632f0f94136b0b132a79c09b8e881db0f9c25d.jpg","pages":1,"instant_server":"chat.bilibili.com","created":1489650761,"created_at":"2017-03-16 15:52","credit":"--","coins":6868,"spid":null,"src":"c","cid":15195741,"partname":"\u6700\u7ec8_x264","part":"\u6700\u7ec8_x264","from":"vupload","type":"vupload","vid":"vupload_15195741","offsite":"https:\/\/share.b23.tv\/flash.swf?aid=9196627&page=1","list":[{"page":1,"type":"vupload","part":"\u6700\u7ec8_x264","cid":15195741,"weblink":"","vid":"","has_alias":false}]} 

----------------------------------------------------
DEBUG:extractor.py:195:root:query: {"image": "https://i0.hdslb.com/bfs/archive/f2b6833f8d732c6b624e11572b9b86afac7d9687.jpg", "vid": 15195741, "title": "【补帧向/AMV】一花一草一世界", "page": 1, "tvid": "9196627", "hd": 6, "parse": "https://www.bilibili.com/video/av9196627/", "type": "bilibili", "category": "video"}
----------------------------------------------------
DEBUG:common.py:324:requests:get
url: https://app.bilibili.com/v2/playurl?appkey=iVGUTjsxvpLeuDCf&build=4140&buvid=ef5efdc0452641eb235cd424dfa03660&cid=15195741&device=phone&otype=json&platform=html5&qn=80&type=mp4&sign=d6f949304746364a1f53fdedf68d676a
useragent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.13; rv:67.0) Gecko/20100101 Firefox/67.0
----------------------------------------------------
DEBUG:bilibili.py:174:parse:getMp4Source: {"from":"local","result":"suee","quality":48,"format":"hdmp4","timelength":128021,"accept_format":"hdmp4,mp4,mp4","accept_description":["高清 720P","流畅 360P","极速 240P"],"accept_quality":[48,16,6],"video_codecid":7,"video_project":true,"seek_param":"start","seek_type":"second","durl":[{"order":1,"length":128021,"size":20025602,"url":"http://upos-sz-mirrorkodo.bilivideo.com/upgcxcode/41/57/15195741/15195741-1-48.mp4?e=ig8euxZM2rNcNbhHhwdVhoMznWdVhwdEto8g5X10ugNcXBB_&deadline=1609912489&gen=playurl&nbs=1&oi=2016110196&os=kodobv&platform=html5&trid=ba049c012a19485496916f65bf9edef3&uipk=5&upsig=a54cdd16c893340314d8c5f7aac83298&uparams=e,deadline,gen,nbs,oi,os,platform,trid,uipk&mid=0"}]} 

----------------------------------------------------
DEBUG:common.py:324:requests:get
url: https://interface.bilibili.com/v2/playurl?appkey=iVGUTjsxvpLeuDCf&build=4140&buvid=ef5efdc0452641eb235cd424dfa03660&cid=15195741&device=phone&otype=json&platform=html5&qn=80&quality=80&type=flv&sign=b03263f612a951ee889b5e0d0f472ca7
useragent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.13; rv:67.0) Gecko/20100101 Firefox/67.0
----------------------------------------------------
DEBUG:common.py:324:requests:get
url: https://interface.bilibili.com/v2/playurl?appkey=iVGUTjsxvpLeuDCf&build=4140&buvid=ef5efdc0452641eb235cd424dfa03660&cid=15195741&device=phone&otype=json&platform=html5&qn=74&quality=74&type=flv&sign=3a203730759d96ecc02f62e95cd52b74
useragent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.13; rv:67.0) Gecko/20100101 Firefox/67.0
----------------------------------------------------
DEBUG:bilibili.py:230:parse:getFlvSource: {"from":"local","result":"suee","quality":64,"format":"flv720","timelength":128143,"accept_format":"flv720_p60,flv,flv720,flv480,flv360","accept_description":["高清 720P60","高清 1080P","高清 720P","清晰 480P","流畅 360P"],"accept_quality":[74,80,64,32,16],"video_codecid":7,"video_project":true,"seek_param":"start","seek_type":"offset","durl":[{"order":1,"length":128143,"size":26408334,"url":"http://upos-sz-mirrorcos.bilivideo.com/upgcxcode/41/57/15195741/15195741_da3-1-64.flv?e=ig8euxZM2rNcNbU17WdVhoMBhWUVhwdEto8g5X10ugNcXBB_&deadline=1609912489&gen=playurl&nbs=1&oi=2016110196&os=cosbv&platform=html5&trid=e2929defeb594dad8018b170518f4c8d&uipk=5&upsig=da9ad200e8838345be248de95733c48c&uparams=e,deadline,gen,nbs,oi,os,platform,trid,uipk&mid=0"}]} 

----------------------------------------------------
{
    "category": "video",
    "duration": 128.143,
    "ext": "flv",
    "extra": {
        "header": {
            "Referer": "https://www.bilibili.com/video/",
            "User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.13; rv:71.0) Gecko/20100101 Firefox/71.0"
        },
        "headers": {
            "User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.13; rv:68.0) Gecko/20100101 Firefox/68.0"
        },
        "playback": "flv"
    },
    "hd": 4,
    "image": "https://i0.hdslb.com/bfs/archive/f2b6833f8d732c6b624e11572b9b86afac7d9687.jpg",
    "multirates": 4,
    "otype": "video",
    "page": 1,
    "parse": "https://www.bilibili.com/video/av9196627/",
    "playback": "mp4",
    "quality": [
        "流畅 360P",
        "清晰 480P",
        "高清 720P",
        "高清 1080P"
    ],
    "show": "高清 1080P",
    "site": "哔哩哔哩(BILIBILI)",
    "size": 26408334,
    "streams": {
        "flv": "http://upos-sz-mirrorcos.bilivideo.com/upgcxcode/41/57/15195741/15195741_da3-1-64.flv?e=ig8euxZM2rNcNbU17WdVhoMBhWUVhwdEto8g5X10ugNcXBB_&deadline=1609912489&gen=playurl&nbs=1&oi=2016110196&os=cosbv&platform=html5&trid=e2929defeb594dad8018b170518f4c8d&uipk=5&upsig=da9ad200e8838345be248de95733c48c&uparams=e,deadline,gen,nbs,oi,os,platform,trid,uipk&mid=0",
        "mp4": "http://upos-sz-mirrorkodo.bilivideo.com/upgcxcode/41/57/15195741/15195741-1-48.mp4?e=ig8euxZM2rNcNbhHhwdVhoMznWdVhwdEto8g5X10ugNcXBB_&deadline=1609912489&gen=playurl&nbs=1&oi=2016110196&os=kodobv&platform=html5&trid=ba049c012a19485496916f65bf9edef3&uipk=5&upsig=a54cdd16c893340314d8c5f7aac83298&uparams=e,deadline,gen,nbs,oi,os,platform,trid,uipk&mid=0",
        "segs": [
            {
                "duration": 128.143,
                "size": 26408334,
                "url": "http://upos-sz-mirrorcos.bilivideo.com/upgcxcode/41/57/15195741/15195741_da3-1-64.flv?e=ig8euxZM2rNcNbU17WdVhoMBhWUVhwdEto8g5X10ugNcXBB_&deadline=1609912489&gen=playurl&nbs=1&oi=2016110196&os=cosbv&platform=html5&trid=e2929defeb594dad8018b170518f4c8d&uipk=5&upsig=da9ad200e8838345be248de95733c48c&uparams=e,deadline,gen,nbs,oi,os,platform,trid,uipk&mid=0"
            }
        ]
    },
    "title": "【补帧向 AMV】一花一草一世界",
    "tvid": "9196627",
    "type": "bilibili",
    "vid": 15195741
}

```
**读取文本TXT (TEXT)**

```
urls.txt格式

http://www.le.com/ptv/vplay/1277143.html
1277145
1277142
http://www.le.com/ptv/vplay/1277141.html

$ vparse ./urls.txt -t le 
```

 
**读取文本JSON (JSON)**

```
urls.json格式
[{"parse":"https://www.bilibili.com/video/av9196627/"},{"parse":"15195741","type":"bilibil"},{"parse":url,"type":type,"proxy":proxy}....]
$ vparse ./urls.json

[id1,id2,id3,id4]
$ vparse ./urls.json -t type
```


**-ts --start, -te --end, -tl length, -fs --fullscreen (FFMPEG/MPV)**
```
$ vparse http://www.le.com/ptv/vplay/1277143.html -p mpv -ts 60 -te 120
$ vparse http://www.le.com/ptv/vplay/1277143.html -p mpv -ts 60 -tl 20
$ vparse http://www.le.com/ptv/vplay/1277143.html -p mpv -ts 60  
$ vparse http://www.le.com/ptv/vplay/1277143.html -d -ts 60 -te 120
$ vparse http://www.le.com/ptv/vplay/1277143.html -d -ts 60 -tl 20
$ vparse http://www.le.com/ptv/vplay/1277143.html -d -ts 60 
```
**-a --capture : 片段截取 (Ffmpeg capture fragment )**

```
# 和-d模式不一样,-d会下载所有分段后再合并整段,再根据-ts -te -tl 对视频进行截取
# -a模式下,ffmpeg录制对象为playback(mp4,m3u8,flv...),再根据-ts -te -tl 对视频进行截取

$ vparse http://www.le.com/ptv/vplay/1277143.html -a -ts 60 -te 120
```
**-itag --itag : YouTube使用 (Youtube itag)**
```
$ vparse https://www.youtube.com/watch?v=zBKei6Ji_WI -itag 315:251 -p mpv
$ vparse https://www.youtube.com/watch?v=zBKei6Ji_WI -itag 315:251 -d -f mp4
$ vparse https://www.youtube.com/watch?v=zBKei6Ji_WI -itag 315:251 -a ts 60 -te 120
```