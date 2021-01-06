# 解析说明
## 解析函数
**只需在collect.py设定函数返回参数列表,打包函数会自动获取参数列表中的数据,不需要额外return 
等同PHP的compact函数**
```
def query(self, p):
    logger = self.logging.getLogger('query')
    common = self.common
    if p.get("query"):
        title= 'test'
        duration= 123
        image = 'https://xxx.com/xxx/x.jpg'
    return self.compact('query')


def parse(self, p):
    logger = self.logging.getLogger('parse')
    common = self.common
    assert p['vid'], "vid"
    vid = p['vid']
    
    mp4 = 'http://xxx.com/xx/x.mp4'
    m3u8 = 'http://xxx.com/xx/x.mp4'
    segs = [{'url':mp4_1},{'url':mp4_2}]
    ext = 'mp4'
    playback = 'm3u8'
    
    ###
    title= 'test'
    duration= 123
    image = 'https://xxx.com/xxx/x.jpg'

    return self.compact('parse')

```
## 打包函数

```    
def compact(self, funcName):
    params = getattr(collect, funcName)(self.params["category"])
    locals = sys._getframe(1).f_locals
    inter = set(params).intersection(set(locals.keys()))
    return collect.stream(locals, inter, funcName)
```
