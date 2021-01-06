# 参数说明
## 视频:
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

| 参数 | 说明 |
| --- | --- |
| duration | 时长 |
| ext | 下载格式 |
| hd | 当前要解析的分辨率索引 |
| image | 图片 |
| multirates  | 当前提供多少分辨率选项可供下载 |
| parse | 解析链接 |
| pay | 是否会员可看 |
| playback | 播放格式 |
| quality | 当前资源可提供的分辨率列表 |
| show | 当前下载分辨率名称 |
| streams | 下载数据 |
| mp4 | 解析包含mp4 |
| m3u8 | 解析包含m3u8 |
| segs | duration:切片时长(空) size:切片大小(空) url:切片链接 |
| title | 标题 |
| type | 链接所属域名 |
| vid | 解析vid |
| category | 链接所属分类,视频/直播/音乐|
