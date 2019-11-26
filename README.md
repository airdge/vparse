
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
{'title': '刀剑神域 爱丽丝篇 异界战争 第5集 开战前夜', 'image': 'http://pic7.iqiyipic.com/image/20191110/ed/52/v_140769663_m_601_m1_480_270.jpg', 'vid': '1f744786c7f4b15d4ec70b08d030bbfd', 'tvid': '9177088900', 'pay': '', 'duration': 1445, 'hd': 5, 'parse': 'https://www.iqiyi.com/v_19rv876x9k.html', 'type': 'iqiyi', 'vtype': 'video', 'streams': {'segs': [{'url': 'http://cache.m.iqiyi.com/mus/246382101/3dfabf1047a5363e76c72e12fece8764/afbe8fd3d73448c9//20191107/00/78/ef4f5563bef229be82c368d0cb153807.m3u8', 'duration': 1445, 'size': 325434438}], 'm3u8': 'http://cache.m.iqiyi.com/mus/246382101/3dfabf1047a5363e76c72e12fece8764/afbe8fd3d73448c9//20191107/00/78/ef4f5563bef229be82c368d0cb153807.m3u8'}, 'quality': ['极速', '流畅', '高清', '720P', '1080P', '1080P50'], 'multirates': 6, 'show': '1080P', 'playType': 'm3u8', 'ext': 'm3u8'}
```
**读取文本链接 暂只支持txt格式**

```
urls.txt格式

http://www.le.com/ptv/vplay/1277143.html
1277145
1277142
http://www.le.com/ptv/vplay/1277141.html
```

```
$ vparse ./urls.txt -t le -q -j
{
    "hd": 5,
    "image": "http://i2.letvimg.com/lc09_yunzhuanma/201611/16/11/57/5718cbc33bd8c2cd6270066c73a187ce_v2_MjcwMzgzOA==/thumb/5_640_320.jpg",
    "parse": "http://www.le.com/ptv/vplay/1277143.html",
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
    "parse": "http://www.le.com/ptv/vplay/1277141.html",
    "title": "钢之炼金术师FA 第04话",
    "tvid": "1351417",
    "type": "le",
    "vid": "1277141",
    "vtype": "video"
}
```
**一次获取多个解析**

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
    "vtype": "video"
}
{
    "hd": 5,
    "image": "http://i1.letvimg.com/lc12_yunzhuanma/201611/16/14/39/83093e33235cbf0cc403994073d5affa_v2_MjcwMzgzNg==/thumb/6_640_320.jpg",
    "parse": "http://www.le.com/ptv/vplay/1277142.html",
    "title": "钢之炼金术师FA 第03话",
    "tvid": "1351418",
    "type": "le",
    "vid": "1277142",
    "vtype": "video"
}
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

Hls: http://cache.m.iqiyi.com/mus/246382101/3dfabf1047a5363e76c72e12fece8764/afbe8fd3d73448c9//20191107/00/78/ef4f5563bef229be82c368d0cb153807.m3u8


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
        "m3u8": "http://cache.m.iqiyi.com/mus/246382101/b4963ee84fbc9342ea3b1fac0c25b8dc/afbe8fd3d73448c9/1725925222/20191121/ce/d7/4f5259ad6061c40783b8eff7911b6267.m3u8",
        "segs": [
            {
                "duration": 1445,
                "size": 344350624,
                "url": "http://cache.m.iqiyi.com/mus/246382101/b4963ee84fbc9342ea3b1fac0c25b8dc/afbe8fd3d73448c9/1725925222/20191121/ce/d7/4f5259ad6061c40783b8eff7911b6267.m3u8"
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
$ vparse https://www.youtube.com/watch?v=p50QboBtZ5w -x socks5://127.0.0.1:1080 -j
$ vparse https://www.youtube.com/watch?v=p50QboBtZ5w -x 127.0.0.1:10800 -j
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
        "mp4": "https://r4---sn-i3b7knlk.googlevideo.com/videoplayback?expire=1574584588&ei=rOzZXaToEYz84wKn6ZqIA",
        "segs": [
            {
                "url": "https://r4---sn-i3b7knlk.googlevideo.com/videoplayback?expire=1574584588&ei=rOzZXaToEYz84wKn6ZqIAg"
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
$ vparse http://www.le.com/comic/45402.html -l -q -j -b -4
$ vparse http://www.le.com/comic/45402.html -l -q -j -b 60
  
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


Playing: http://cache.m.iqiyi.com/mus/246382101/3dfabf1047a5363e76c72e12fece8764/afbe8fd3d73448c9//20191107/00/78/ef4f5563bef229be82c368d0cb153807.m3u8
```
**-s : 调试**

```
$ vparse http://www.le.com/ptv/vplay/1277143.html -s -j
DEBUG:root:query: {"vid": "1277143", "hd": 5, "parse": "http://www.le.com/ptv/vplay/1277143.html", "type": "le", "vtype": "video"}

DEBUG:urllib3.connectionpool:Starting new HTTP connection (1): player-pc.le.com:80
DEBUG:urllib3.connectionpool:http://player-pc.le.com:80 "GET /mms/out/video/playJson?id=1277143&platid=1&splatid=105&format=1&tkey=2639962097&domain=www.le.com&region=cn&source=1000&accessyx=1&tss=ios HTTP/1.1" 200 None
DEBUG:parse:data: {"code": 1, "msgs": {"playurl": {"videoType": {"180001": "\u6b63\u7247"}, "cid": "5", "pid": 45402, "vid": 1277143, "mid": ",1351419,", "title": "\u94a2\u4e4b\u70bc\u91d1\u672f\u5e08FA \u7b2c01\u8bdd", "picAll": {"640*320": "http://i2.letvimg.com/lc09_yunzhuanma/201611/16/11/57/5718cbc33bd8c2cd6270066c73a187ce_v2_MjcwMzgzOA==/thumb/5_640_320.jpg", "400*300": "http://i2.letvimg.com/lc09_yunzhuanma/201611/16/11/57/5718cbc33bd8c2cd6270066c73a187ce_v2_MjcwMzgzOA==/thumb/5_400_300.jpg", "300*400": "http://i2.letvimg.com/lc09_yunzhuanma/201611/16/11/57/5718cbc33bd8c2cd6270066c73a187ce_v2_MjcwMzgzOA==/thumb/5_300_400.jpg", "400*225": "http://i2.letvimg.com/lc09_yunzhuanma/201611/16/11/57/5718cbc33bd8c2cd6270066c73a187ce_v2_MjcwMzgzOA==/thumb/5_400_225.jpg", "400*250": "http://i2.letvimg.com/lc09_yunzhuanma/201611/16/11/57/5718cbc33bd8c2cd6270066c73a187ce_v2_MjcwMzgzOA==/thumb/5_400_250.jpg"}, "pic": "http://i2.letvimg.com/lc09_yunzhuanma/201611/16/11/57/5718cbc33bd8c2cd6270066c73a187ce_v2_MjcwMzgzOA==/thumb/5_120_90.jpg", "download": ["290002", "290003", "290005"], "total": 64, "nextvid": 1277145, "subtitle": "", "domain": ["http://play.g3proxy.lecloud.com", "http://bplay.g3proxy.lecloud.com", "http://123.59.235.111"], "dispatch": {"350": ["/vod/v2/MjMwLzcvMTAxL2xldHYtdXRzLzE0L3Zlcl8wMF8yMi0xMDcyODE2NTIzLWF2Yy0yMDAxMDctYWFjLTMyMDAzLTE0NjczMDEtNDQzNTcxNTYtMzc0MDczNTFiNTgzNjEyYjA4YWUyMzY1MjllOGIyMDUtMTQ3OTI2ODY3NzEyNi5tcDQ=?b=241&mmsid=1351419"], "1000": ["/vod/v2/MjM4LzQ4LzkxL2xldHYtdXRzLzE0L3Zlcl8wMF8yMi0xMDcyODE2NTI3LWF2Yy0zOTAyOTItYWFjLTMyMDAzLTE0NjczMDEtNzkyNDA3NTgtZTA1ZWNmYTE0ZjZlMzJmYWYwZmRmZGUwNDViNzc2YjYtMTQ3OTI2ODU3MDI0OC5tcDQ=?b=432&mmsid=1351419"]}, "duration": 1467}, "drmFlag": false, "point": {"hot": {}, "skip": [0, 0]}, "paylist": ["1080p"], "firstlook": "0", "playstatus": {"status": "1"}, "isTryLook": "0", "danmu": 1, "watermark": {"imgs": [{"lasttime": "1800", "link": "", "position": "2", "url100": "http://i1.letvimg.com/lc04_iscms/201601/12/15/22/47615b27e213449da27bfd356df13f38.png"}, {"lasttime": "1800", "link": "", "position": "1", "url100": "http://i0.letvimg.com/lc04_iscms/201601/12/15/22/afd7ca79d3564037acd9606ce04069c2.png"}], "offset": "3"}, "statuscode": 1001, "vtypeFlag": false, "curVType": "1000", "trylook": 0, "trylookTime": 0}}

{
    "duration": 1467,
    "ext": "m3u8",
    "hd": 2,
    "multirates": 2,
    "parse": "http://www.le.com/ptv/vplay/1277143.html",
    "playType": "m3u8",
    "quality": [
        "流畅",
        "标清"
    ],
    "show": "标清",
    "streams": {
        "extra": {
            "header": {
                "Accept": "*/*",
                "Accept-Language": "zh-cn",
                "Cache-Control": "no-cache",
                "Pragma": "no-cache",
                "User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.13; rv:68.0) Gecko/20100101 Firefox/68.0"
            }
        },
        "m3u8": "http://play.g3proxy.lecloud.com//vod/v2/MjM4LzQ4LzkxL2xldHYtdXRzLzE0L3Zlcl8wMF8yMi0xMDcyODE2NTI3LWF2Yy0zOTAyOTItYWFjLTMyMDAzLTE0NjczMDEtNzkyNDA3NTgtZTA1ZWNmYTE0ZjZlMzJmYWYwZmRmZGUwNDViNzc2YjYtMTQ3OTI2ODU3MDI0OC5tcDQ=?b=432&mmsid=1351419",
        "segs": [
            {
                "duration": 1467,
                "url": "http://play.g3proxy.lecloud.com//vod/v2/MjM4LzQ4LzkxL2xldHYtdXRzLzE0L3Zlcl8wMF8yMi0xMDcyODE2NTI3LWF2Yy0zOTAyOTItYWFjLTMyMDAzLTE0NjczMDEtNzkyNDA3NTgtZTA1ZWNmYTE0ZjZlMzJmYWYwZmRmZGUwNDViNzc2YjYtMTQ3OTI2ODU3MDI0OC5tcDQ=?b=432&mmsid=1351419"
            }
        ]
    },
    "title": "钢之炼金术师FA 第01话",
    "type": "le",
    "vid": "1277143",
    "vtype": "video"
}

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
