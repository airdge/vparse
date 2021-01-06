## EXTRA
**extra参数是给下载(download)或播放(player)提供相应参数说明**
```
        extra = {
            "reload": 3,
            "language" :[
                {
                    "langcode": "ja",
                    "language": "日语",
                    "url": "https://v.youku.com/v_show/id_XMjk4NzA1OTMzNg==.html"
                },
                {
                    "langcode": "guoyu",
                    "language": "普通话",
                    "url": "https://v.youku.com/v_show/id_XMjk4NzA1OTE0NA==.html"
                }
            ], 
            "cookie": cookie,
            "referer": url,
            "useragent": useraget,
            "headers": {
                "User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.13; rv:68.0) Gecko/20100101 Firefox/68.0",
                "Accept": "*/*",
                "Accept-Language": "zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2",
                "Accept-Encoding": "gzip, deflate, br",
                "Referer": "https://www/",
                "Origin": "https://www/",
                "Connection": "keep-alive",
                "Cookie": "cookie",
            },
```
## 参数
| 参数 | 数值 | 说明(都是非必要,需要添加) |
| --- | --- | --- |
| reload | int | 腾讯视频限速解决方案,每循环下载reload个片段,重新解析替换原segs数据 |
| language | dict | 多语言提示, langcode:语言(英)  language:语言  url:链接 |
| cookie<div>referer<div>useragent<div>encoding | str | 默认空,如果没有添加headers,可以单独设置 |
| header | dict | 下载与播放使用请求头 |
| player | str | 默认空,temp边下边播 |

## 示例

```
# qq.py

  extra = {"reload": 3}
```
```
# bilibili.py

    extra = {
        "headers": {
            "User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.13; rv:71.0) Gecko/20100101 Firefox/71.0",
            "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8",
            "Accept-Language": "zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2",
            "Referer": url,
        }
    }
    
     

```
