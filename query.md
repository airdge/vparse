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

| 参数 | 说明 |
| --- | --- |
| duration | 时长 |
| ext | 下载格式 |
| hd | 当前解析分辨率数值大小 |
| image | 图片 |
| multirates  | 当前视频有多少分辨率选项可下载 |
| parse | 解析链接 |
| pay | 是否会员可看 |
| playType | 播放格式 |
| show | 当前下载的分辨率名称 |
| streams | 下载数据 |
| mp4 | 解析包含mp4 |
| m3u8 | 解析包含m3u8 |
| segs | duration:切片时长 size:切片大小 url:切片链接 |
| title | 标题 |
| tvid | 视频tvid(如果有) |
| type | 视频site(类型) |
| vid | 视频解析vid |
| vtype | 视频形式 音乐 视频  直播 |
