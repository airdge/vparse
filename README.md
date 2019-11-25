
## 版本要求
**python>=3.6**
## 扩展依赖

```'
requests', 'pycryptodome', 'pysocks','gevent','pyexecjs'
```
**如果你的操作环境支持[quickjs](https://github.com/PetterS/quickjs),请先安装**
## 使用说明
**默认打印JSON**
```
$ vparse https://www.iqiyi.com/v_19rv876x9k.html
{'title': '刀剑神域 爱丽丝篇 异界战争 第5集 开战前夜', 'image': 'http://pic7.iqiyipic.com/image/20191110/ed/52/v_140769663_m_601_m1_480_270.jpg', 'vid': '1f744786c7f4b15d4ec70b08d030bbfd', 'tvid': '9177088900', 'pay': '', 'duration': 1445, 'hd': 5, 'parse': 'https://www.iqiyi.com/v_19rv876x9k.html', 'type': 'iqiyi', 'vtype': 'video', 'streams': {'segs': [{'url': 'http://cache.m.iqiyi.com/mus/246382101/3dfabf1047a5363e76c72e12fece8764/afbe8fd3d73448c9//20191107/00/78/ef4f5563bef229be82c368d0cb153807.m3u8?vt=0&qd_uri=dash&qd_time=1574560984989&qd_originate=pcw&code=2&bossStatus=0&src=01080031010000000000&tm=1574560983000&ff=ts&tvid=9177088900&qd_vip=1&sgti=14_0bf07aa57b104186c904feafd1a0a935_1574560983000&k_uid=0bf07aa57b104186c904feafd1a0a935&px=&_lnt=0&vf=92e648f96498d3641ba845968934c119', 'duration': 1445, 'size': 325434438}], 'm3u8': 'http://cache.m.iqiyi.com/mus/246382101/3dfabf1047a5363e76c72e12fece8764/afbe8fd3d73448c9//20191107/00/78/ef4f5563bef229be82c368d0cb153807.m3u8?vt=0&qd_uri=dash&qd_time=1574560984989&qd_originate=pcw&code=2&bossStatus=0&src=01080031010000000000&tm=1574560983000&ff=ts&tvid=9177088900&qd_vip=1&sgti=14_0bf07aa57b104186c904feafd1a0a935_1574560983000&k_uid=0bf07aa57b104186c904feafd1a0a935&px=&_lnt=0&vf=92e648f96498d3641ba845968934c119'}, 'quality': ['极速', '流畅', '高清', '720P', '1080P', '1080P50'], 'multirates': 6, 'show': '1080P', 'playType': 'm3u8', 'ext': 'm3u8'}
```
**-d : 下载**
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

Hls: http://cache.m.iqiyi.com/mus/246382101/3dfabf1047a5363e76c72e12fece8764/afbe8fd3d73448c9//20191107/00/78/ef4f5563bef229be82c368d0cb153807.m3u8?vt=0&qd_uri=dash&qd_time=1574561688391&qd_originate=pcw&code=2&bossStatus=0&src=01080031010000000000&tm=1574561687000&ff=ts&tvid=9177088900&qd_vip=1&sgti=14_b3280dcbb45876c88b43ce4baefbee49_1574561687000&k_uid=b3280dcbb45876c88b43ce4baefbee49&px=&_lnt=0&vf=cf712ca29e81048055c2a2d99ef05820


[1 / 190] |-████████████████████████████████-|100%  2170.78kb/s 0.73M/0.85M 
[2 / 190] |-███████████████████████████████--|98%  144.80kb/s 2.51M/2.56M
```
**-j : 打印格式化JSON**
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
    "playType": "m3u8",
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
        "m3u8": "http://cache.m.iqiyi.com/mus/246382101/3dfabf1047a5363e76c72e12fece8764/afbe8fd3d73448c9//20191107/00/78/ef4f5563bef229be82c368d0cb153807.m3u8?vt=0&qd_uri=dash&qd_time=1574561192791&qd_originate=pcw&code=2&bossStatus=0&src=01080031010000000000&tm=1574561191000&ff=ts&tvid=9177088900&qd_vip=1&sgti=14_1aa9e86e9876f9368780bfe6d95f98b7_1574561191000&k_uid=1aa9e86e9876f9368780bfe6d95f98b7&px=&_lnt=0&vf=73ea88886dd8ee8fb40a955042a624d0",
        "segs": [
            {
                "duration": 1445,
                "size": 325434438,
                "url": "http://cache.m.iqiyi.com/mus/246382101/3dfabf1047a5363e76c72e12fece8764/afbe8fd3d73448c9//20191107/00/78/ef4f5563bef229be82c368d0cb153807.m3u8?vt=0&qd_uri=dash&qd_time=1574561192791&qd_originate=pcw&code=2&bossStatus=0&src=01080031010000000000&tm=1574561191000&ff=ts&tvid=9177088900&qd_vip=1&sgti=14_1aa9e86e9876f9368780bfe6d95f98b7_1574561191000&k_uid=1aa9e86e9876f9368780bfe6d95f98b7&px=&_lnt=0&vf=73ea88886dd8ee8fb40a955042a624d0"
            }
        ]
    },
    "title": "刀剑神域 爱丽丝篇 异界战争 第5集 开战前夜",
    "tvid": "9177088900",
    "type": "iqiyi",
    "vid": "1f744786c7f4b15d4ec70b08d030bbfd",
    "vtype": "video"
}
```
**-r : 获取其他分辨率解析链接**

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
    "playType": "m3u8",
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
        "m3u8": "http://cache.m.iqiyi.com/mus/246382101/e0af4c681ed3af040f893d7cb249efcf/afbe8fd3d73448c9//20191107/30/5b/433b7103cdaa1a6e542f88bc491ed6d5.m3u8?vt=0&qd_uri=dash&qd_time=1574563138612&qd_originate=pcw&code=2&bossStatus=0&src=01080031010000000000&tm=1574563137000&ff=ts&tvid=9177088900&qd_vip=1&sgti=14_14d58671a39af104554307e66954eb35_1574563137000&k_uid=14d58671a39af104554307e66954eb35&px=&_lnt=0&vf=60251dbc471dc21994508da4dda2c854",
        "segs": [
            {
                "duration": 1445,
                "size": 28441560,
                "url": "http://cache.m.iqiyi.com/mus/246382101/e0af4c681ed3af040f893d7cb249efcf/afbe8fd3d73448c9//20191107/30/5b/433b7103cdaa1a6e542f88bc491ed6d5.m3u8?vt=0&qd_uri=dash&qd_time=1574563138612&qd_originate=pcw&code=2&bossStatus=0&src=01080031010000000000&tm=1574563137000&ff=ts&tvid=9177088900&qd_vip=1&sgti=14_14d58671a39af104554307e66954eb35_1574563137000&k_uid=14d58671a39af104554307e66954eb35&px=&_lnt=0&vf=60251dbc471dc21994508da4dda2c854"
            }
        ]
    },
    "title": "刀剑神域 爱丽丝篇 异界战争 第5集 开战前夜",
    "tvid": "9177088900",
    "type": "iqiyi",
    "vid": "1f744786c7f4b15d4ec70b08d030bbfd",
    "vtype": "video"
}
```
**-q : 只获取链接信息,不获取解析地址**
```
$ vparse https://www.iqiyi.com/v_19rv876x9k.html -j -q
{
    "duration": 1445,
    "hd": 5,
    "image": "http://pic7.iqiyipic.com/image/20191110/ed/52/v_140769663_m_601_m1_480_270.jpg",
    "parse": "https://www.iqiyi.com/v_19rv876x9k.html",
    "pay": "",
    "title": "刀剑神域 爱丽丝篇 异界战争 第5集 开战前夜",
    "tvid": "9177088900",
    "type": "iqiyi",
    "vid": "1f744786c7f4b15d4ec70b08d030bbfd",
    "vtype": "video"
}
```
**-c : 传入cookie 支持文本或字符串**

```
$ vparse https://www.iqiyi.com/v_19rvasnkfk.html -c ./iqiyi.txt -j
$ vparse https://www.iqiyi.com/v_19rvasnkfk.html -c "name=value; name2=value2;" -j
{
    "duration": 1445,
    "ext": "m3u8",
    "hd": 5,
    "image": "http://pic9.iqiyipic.com/image/20191122/e6/27/v_141453767_m_601_480_270.jpg",
    "multirates": 6,
    "parse": "https://www.iqiyi.com/v_19rvasnkfk.html",
    "pay": "1",
    "playType": "m3u8",
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
        "m3u8": "http://cache.m.iqiyi.com/mus/246382101/b4963ee84fbc9342ea3b1fac0c25b8dc/afbe8fd3d73448c9/1725925222/20191121/ce/d7/4f5259ad6061c40783b8eff7911b6267.m3u8?vt=0&qd_uri=dash&qd_time=1574562021299&bossStatus=2&_lnt=0&prv=0&qd_originate=pcw&code=2&ff=ts&px=&tm=1574562020000&previewType=3&src=01080031010000000000&qd_vip=1&tvid=9623313500&k_uid=dafec0530e6aab2b4a9fd84b65f70b7d&previewTime=0&sgti=14_dafec0530e6aab2b4a9fd84b65f70b7d_1574562020000&vf=d182e926dd8dc966394685562a60ad26",
        "segs": [
            {
                "duration": 1445,
                "size": 344350624,
                "url": "http://cache.m.iqiyi.com/mus/246382101/b4963ee84fbc9342ea3b1fac0c25b8dc/afbe8fd3d73448c9/1725925222/20191121/ce/d7/4f5259ad6061c40783b8eff7911b6267.m3u8?vt=0&qd_uri=dash&qd_time=1574562021299&bossStatus=2&_lnt=0&prv=0&qd_originate=pcw&code=2&ff=ts&px=&tm=1574562020000&previewType=3&src=01080031010000000000&qd_vip=1&tvid=9623313500&k_uid=dafec0530e6aab2b4a9fd84b65f70b7d&previewTime=0&sgti=14_dafec0530e6aab2b4a9fd84b65f70b7d_1574562020000&vf=d182e926dd8dc966394685562a60ad26"
            }
        ]
    },
    "title": "刀剑神域 爱丽丝篇 异界战争 第7集 失格者的烙印",
    "tvid": "9623313500",
    "type": "iqiyi",
    "vid": "6eb556fe2904233bf251762fef850332",
    "vtype": "video"
}
```
**-t : urls为id形式时使用**
```
$ vparse 9177088900 -t iqiyi -q -j
{
    "duration": 1445,
    "hd": 5,
    "image": "http://pic7.iqiyipic.com/image/20191110/ed/52/v_140769663_m_601_m1_480_270.jpg",
    "parse": "9177088900",
    "pay": "",
    "title": "刀剑神域 爱丽丝篇 异界战争 第5集 开战前夜",
    "tvid": "9177088900",
    "type": "iqiyi",
    "vid": "1f744786c7f4b15d4ec70b08d030bbfd",
    "vtype": "video"
}
```
**-x : proxy代理**

```
vparse https://www.youtube.com/watch?v=p50QboBtZ5w -x socks5://127.0.0.1:1080 -j
vparse https://www.youtube.com/watch?v=p50QboBtZ5w -x 127.0.0.1:10800 -j
{
    "duration": "2602",
    "ext": "mp4",
    "hd": 1,
    "image": "https://i.ytimg.com/vi/p50QboBtZ5w/hqdefault.jpg?sqp=-oaymwEZCNACELwBSFXyq4qpAwsIARUAAIhCGAFwAQ==&rs=AOn4CLAwFbAgOHErv5ppRwxDt-TDg0cdQg",
    "multirates": 1,
    "parse": "https://www.youtube.com/watch?v=p50QboBtZ5w",
    "playType": "mp4",
    "quality": [
        "medium"
    ],
    "show": "medium",
    "streams": {
        "extra": {
            "download": "extra",
            "encoding": "gzip, deflate, br",
            "header": {
                "Accept": "*/*",
                "Accept-Language": "zh-cn",
                "Cache-Control": "no-cache",
                "Pragma": "no-cache",
                "Referer": "https://www.youtube.com/watch?v=p50QboBtZ5w&app=desktop",
                "User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.13; rv:68.0) Gecko/20100101 Firefox/68.0"
            }
        },
        "mp4": "https://r4---sn-i3b7knlk.googlevideo.com/videoplayback?expire=1574584588&ei=rOzZXaToEYz84wKn6ZqIAg&ip=154.204.42.196&id=o-AM38i-mJfAyCajvGjEOiOemkJDNP46b10bcT9R13fCOA&itag=18&source=youtube&requiressl=yes&mm=31%2C29&mn=sn-i3b7knlk%2Csn-i3beln7r&ms=au%2Crdu&mv=u&mvi=3&pl=24&gcr=hk&mime=video%2Fmp4&gir=yes&clen=104416108&ratebypass=yes&dur=2602.213&lmt=1540434273073546&mt=1574562416&fvip=4&fexp=23842630&c=WEB&txp=5531432&sparams=expire%2Cei%2Cip%2Cid%2Citag%2Csource%2Crequiressl%2Cgcr%2Cmime%2Cgir%2Cclen%2Cratebypass%2Cdur%2Clmt&lsparams=mm%2Cmn%2Cms%2Cmv%2Cmvi%2Cpl&lsig=AHylml4wRgIhAJl1EeNWEWwMtJgCI9pg71Z31U9ssKn2E0ffKD8BNDpYAiEA_A3QmTyGsZiEoDn6o5gNxwpVZFkMZutWBoTMny6ESq4%3D",
        "segs": [
            {
                "url": "https://r4---sn-i3b7knlk.googlevideo.com/videoplayback?expire=1574584588&ei=rOzZXaToEYz84wKn6ZqIAg&ip=154.204.42.196&id=o-AM38i-mJfAyCajvGjEOiOemkJDNP46b10bcT9R13fCOA&itag=18&source=youtube&requiressl=yes&mm=31%2C29&mn=sn-i3b7knlk%2Csn-i3beln7r&ms=au%2Crdu&mv=u&mvi=3&pl=24&gcr=hk&mime=video%2Fmp4&gir=yes&clen=104416108&ratebypass=yes&dur=2602.213&lmt=1540434273073546&mt=1574562416&fvip=4&fexp=23842630&c=WEB&txp=5531432&sparams=expire%2Cei%2Cip%2Cid%2Citag%2Csource%2Crequiressl%2Cgcr%2Cmime%2Cgir%2Cclen%2Cratebypass%2Cdur%2Clmt&lsparams=mm%2Cmn%2Cms%2Cmv%2Cmvi%2Cpl&lsig=AHylml4wRgIhAJl1EeNWEWwMtJgCI9pg71Z31U9ssKn2E0ffKD8BNDpYAiEA_A3QmTyGsZiEoDn6o5gNxwpVZFkMZutWBoTMny6ESq4%3D"
            }
        ]
    },
    "title": "刀劍神域 Sword Art Online 全OP+ED",
    "type": "youtube",
    "vid": "p50QboBtZ5w",
    "vtype": "video"
}
```
**-l : 列表获取**

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
    "vtype": "video"
}
{
    "hd": 5,
    "image": "http://i3.letvimg.com/lc08_yunzhuanma/201611/16/11/48/bc507343910aedd19c0d194e835151c9_v2_MjcwMzg0Mg==/thumb/6_640_320.jpg",
    "parse": "1277145",
    "title": "钢之炼金术师FA 第02话",
    "tvid": "1351421",
    "type": "le",
    "vid": "1277145",
    "vtype": "video"
}
{
    "hd": 5,
    "image": "http://i1.letvimg.com/lc12_yunzhuanma/201611/16/14/39/83093e33235cbf0cc403994073d5affa_v2_MjcwMzgzNg==/thumb/6_640_320.jpg",
    "parse": "1277142",
    "title": "钢之炼金术师FA 第03话",
    "tvid": "1351418",
    "type": "le",
    "vid": "1277142",
    "vtype": "video"
}
{
    "hd": 5,
    "image": "http://i3.letvimg.com/lc08_yunzhuanma/201611/16/16/33/76362b5277a31258e7bbfc4ee7066b7c_v2_MjcwMzgzNA==/thumb/2_640_320.jpg",
    "parse": "1277141",
    "title": "钢之炼金术师FA 第04话",
    "tvid": "1351417",
    "type": "le",
    "vid": "1277141",
    "vtype": "video"
} 
```
**-o : 列表选择性获取 a,b,c...**

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
    "vtype": "video"
}
{
    "hd": 5,
    "image": "http://i3.letvimg.com/lc13_yunzhuanma/201611/16/15/02/8115319d2a0d790a32cc759780818471_v2_MjcwMzg4NA==/thumb/2_640_320.jpg",
    "parse": "1277166",
    "title": "钢之炼金术师FA 第26话",
    "tvid": "1351442",
    "type": "le",
    "vid": "1277166",
    "vtype": "video"
}
{
    "hd": 5,
    "image": "http://i2.letvimg.com/lc13_yunzhuanma/201611/16/15/47/9aec8f9f7e50d11bbda8cf20b4ba655b_v2_MjcwMzk1OA==/thumb/2_640_320.jpg",
    "parse": "1277203",
    "title": "钢之炼金术师FA 第55话",
    "tvid": "1351479",
    "type": "le",
    "vid": "1277203",
    "vtype": "video"
}
```
**-b : 列表范围获取**

```
$ vparse http://www.le.com/comic/45402.html -l -q -j -b 60,64
  vparse http://www.le.com/comic/45402.html -l -q -j -b -4
  vparse http://www.le.com/comic/45402.html -l -q -j -b 60
  
{
    "hd": 5,
    "image": "http://i0.letvimg.com/lc10_yunzhuanma/201611/16/15/51/5468ea41ea415cfccab75f637f25737a_v2_MjcwMzk2Mg==/thumb/6_640_320.jpg",
    "parse": "1277205",
    "title": "钢之炼金术师FA 第60话",
    "tvid": "1351481",
    "type": "le",
    "vid": "1277205",
    "vtype": "video"
}
{
    "hd": 5,
    "image": "http://i1.letvimg.com/lc09_yunzhuanma/201611/16/17/19/5843a63b4d58ae8e6e09fdbfeb3a0f9e_v2_MjcwMzk0Ng==/thumb/2_640_320.jpg",
    "parse": "1277197",
    "title": "钢之炼金术师FA 第61话",
    "tvid": "1351473",
    "type": "le",
    "vid": "1277197",
    "vtype": "video"
}
{
    "hd": 5,
    "image": "http://i0.letvimg.com/lc12_yunzhuanma/201611/16/17/14/7bbac1994e7ace3ed6ed8213d7269558_v2_MjcwMzk0OA==/thumb/1_640_320.jpg",
    "parse": "1277198",
    "title": "钢之炼金术师FA 第62话",
    "tvid": "1351474",
    "type": "le",
    "vid": "1277198",
    "vtype": "video"
}
{
    "hd": 5,
    "image": "http://i0.letvimg.com/lc12_yunzhuanma/201611/16/17/14/a106117c018094f5feafcaa26434539a_v2_MjcwMzkzOA==/thumb/1_640_320.jpg",
    "parse": "1277193",
    "title": "钢之炼金术师FA 第63话",
    "tvid": "1351469",
    "type": "le",
    "vid": "1277193",
    "vtype": "video"
}
{
    "hd": 5,
    "image": "http://i3.letvimg.com/lc08_yunzhuanma/201611/16/17/15/edd9169755dbc80eda9598ee4431cc32_v2_MjcwMzk1Ng==/thumb/2_640_320.jpg",
    "parse": "1277202",
    "title": "钢之炼金术师FA 第64话",
    "tvid": "1351478",
    "type": "le",
    "vid": "1277202",
    "vtype": "video"
}
```
**-y : 语言选项**

```
$ vparse https://v.youku.com/v_show/id_XMzQ3OTU4NjA3Ng==.html -j -y yue
{
    "duration": 6122.33,
    "ext": "mp4",
    "hd": 4,
    "image": "https://vthumb.ykimg.com/054101015D847F898B6C069AAD259696",
    "multirates": 4,
    "parse": "https://v.youku.com/v_show/id_XMzQ3OTU4NjA3Ng==.html",
    "pay": 1,
    "playType": "m3u8",
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
                    "code": "guoyu",
                    "lang": "普通话",
                    "url": "https://v.youku.com/v_show/id_XMzQ3OTU4NjA3Ng==.html"
                },
                {
                    "code": "yue",
                    "lang": "粤语",
                    "url": "https://v.youku.com/v_show/id_XMzU5NzIxNzg3Mg==.html"
                }
            ]
        },
        "m3u8": "http://pl-ali.youku.com/playlist/m3u8?vid=XMzU5NzIxNzg3Mg%3D%3D&type=mp4hd3v3&ups_client_netip=7d4f14e0&utid=&ccode=0511&psid=21c92c701e39864f23e1735456e46bde&duration=6131&expire=18000&drm_type=1&drm_device=0&ups_ts=1574580289&onOff=0&encr=0&ups_key=caef062325cc4cf654078e295164f94d",
        "segs": [
            {
                "duration": 135.083,
                "url": "http://vali.cp31.ott.cibntv.net/697674F07A333714DB2726E1E/03000C2D005CDEA5757D338055EEB34AD3A715-479C-4458-BCBB-9A88B064C876.mp4?ccode=0511&duration=135&expire=18000&psid=21c92c701e39864f23e1735456e46bde&ups_client_netip=&ups_ts=1574580289&ups_userid=&utid=&vid=XMzU5NzIxNzg3Mg%3D%3D&vkey=Ae91f83997b7c0968bb54fa5d7fcff0f8&s=cc036bd4962411de83b1&sp=&bc=2&dre=u20&si=44"
            },
        ]
    },
    "title": "唐伯虎点秋香[粤语]",
    "type": "youku",
    "vid": "XMzQ3OTU4NjA3Ng==",
    "vtype": "video"
}
```
**-p : 播放器播放**

```
$ vparse https://www.iqiyi.com/v_19rv876x9k.html -p mpv
$ vparse https://www.iqiyi.com/v_19rv876x9k.html -p browser
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


Playing: http://cache.m.iqiyi.com/mus/246382101/3dfabf1047a5363e76c72e12fece8764/afbe8fd3d73448c9//20191107/00/78/ef4f5563bef229be82c368d0cb153807.m3u8?vt=0&qd_uri=dash&qd_time=1574651816157&qd_originate=pcw&code=2&bossStatus=0&src=01080031010000000000&tm=1574651815000&ff=ts&tvid=9177088900&qd_vip=1&sgti=14_9e685d3c0894e82edcb54bae142773b1_1574651815000&k_uid=9e685d3c0894e82edcb54bae142773b1&px=&_lnt=0&vf=419e2f1b4e3ab0adab8719fd3850675d
```
## 参数说明
| 参数 | 数值 | 默认 | 说明 | 英 |
| --- | --- | --- | --- | --- |
| urls | url<div> id |  | 链接<div> id |  |
| -b <div>--beginning | x<div> x,y | False  | 链接是列表时生效<div>若番剧总集为n  <div>参数为x时,解析x到n </div> <div>参数为x,y时,解析x到y |  |
| -c <div>--cookie | string<div>cookie.txt  | False | cookie字符或文本地址 <div>name=value; name2=value2;<div>当传入文本时,支持 Netscape HTTP Cookie File 和 String Cookie |  |
| -d <div>--download |   | store_true  | 执行下载 |  |
| -f<div> —dir | /dir | False | 文件存放目录<div>类型:%type   形式:%vtype<div>支持format time结构化表示<div>%m %d  |  |
| -i <div>--init | backup(b)  <div>restore(r) | False | 初始化设置 <div>参数为b时,备份user.py<div> 参数为r时,还原user.py |  |
| -j <div>--json |  | store_true | 格式化json输出 |  |
| -l <div>--playlist |  | store_true | 说明该解析为播放列表 |  |
| -m <div>--merge | 1<div>0 | 1  |解析分段合并成整段  <div>默认1,下载并合并</div> <div>为0时,只下载不合并    |  |
| -n <div>--name | filename | False | 下载文件名 |  |
| -o <div>--only |   <div>x</div> <div>x,y <div> x,y,z</div> | False | 解析列表时生效  <div>参数为x时,解析x的链接</div> <div>参数为x,y时,解析x和y </div>  |  |
| -p <div>--player | mpv<div> browser | False | 选择播放器<div> mpv或者浏览器 |  |
| -q <div>--query |  | store_true | 只获取视频信息,不获取解析地址 |  |
| -r<div> --hd | 1-7 | False | 分辨率选择   |  |
| -s <div>--debug |  | store_true | 输出调试信息 |  |
| -t <div>--type | bilibili <div> qq | False | 若urls以id形式<div>必须添加 |  |
| -u <div>--multi | 10 <div>  x | False | 下载格式为m3u8<div>启用多线程(伪)下载 |  |
| -v <div>--vtype | video<div> music<div>   live  | False | 区分urls类型<div>直播或音乐或视频<div> 若urls以id形式,必须添加 |  |
| -x<div> —proxy | socks5://x.x.x.x:y <div>x.x.x.x:y | False | 代理服务器<div> http https socks |  |
| -y<div> —-lang |  | False | 国语/粤语...获取 |  |
| -z<div> --timeout | 8 | False | 超时设置 |  |
| -ccode <div>--ccode |  |  | 优酷ccode |  |
| -pwd<div> --pwd |  |  | 视频密码 |  |
## 用户自定义

```
{
        "hd": "5",  # 默认分辨率选择
        "proxy": {  # 代理设置
            "meipai": {
                "video": "socks5://127.0.0.1:1080",
                "music": "",
                "live": ""
            },
            "miaopai": "127.0.0.1:10800"
        },
        "cookie": { # cookie设置
            "qzone": "a=b;c=d;e=f;", 
            "youku": "/usr/youku.tx"
        },
        "change": { # site(type)替换
            "mysohu": "sohu",
            "qiyi": "iqiyi",
            "iask": "sina",
        },
        "quality": { # 分辨率显示输出替换
            "video": {
                "sina": {
                    "sd": "标清",
                    "hd": "高清",
                    "ffd": "超清"
                }
            },
            "music": {
                "migu": {
                    "SQ": "SQ无损",
                    "HQ": "HQ高品质"
                }
            },
        },
        "blacklist": [], # 解析黑名单  'youku','qq'
        "dir": "%vtype/%type", # 默认保存目录 
    }
```
