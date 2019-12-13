## EXTRA
**extra参数是给下载(download)或播放(player)提供相应参数说明**
```
        extra = {
            "reload": 3,
            "language" :[
                {
                    "code": "ja",
                    "lang": "日语",
                    "url": "https://v.youku.com/v_show/id_XMjk4NzA1OTMzNg==.html"
                },
                {
                    "code": "guoyu",
                    "lang": "普通话",
                    "url": "https://v.youku.com/v_show/id_XMjk4NzA1OTE0NA==.html"
                }
            ],
            "download": "merge",
            "cookie": "cookie",
            "referer": "https://www/",
            "useragent": "ua",
            "encoding": "gzip, deflate, sdch",
            "header": {
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
| reload | int | 一般腾讯视频下载三个分段后,会限速. 设置改参数后,会每下载(3)个分段后,重新执行解析,替换原有的streams[‘segs’] 的下载链接,进而达到下载不限速 |
| language | array | 像优酷视频会有多个语言切换. 设置该参数后,会在终端提示该视频有多少语言可选 code:language  lang:语言  url:链接 |
| download | str | 测试功能,可以忽略 |
| cookie<div>referer<div>useragent<div>encoding | str | 请求头参数,如果没有添加header,可以单独设置 |
| header | dict | 请求头 |

## 示例

```
# qq.py

  extra = {"reload": 3}
```
```
# bilibili.py

    extra = {
        "header": {
            "User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.13; rv:71.0) Gecko/20100101 Firefox/71.0",
            "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8",
            "Accept-Language": "zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2",
            "Referer": url,
        }
    }
    
     

```
