# 解析说明
## 解析函数
**只需在函数里设定相应名称的参数,不用多余return 
详见collect.py**
```
def query(self, p):
    logger = self.logging.getLogger('query')
    common = self.common
    if p['query']:
        title= 'test'
        duration= 123
        image = 'https://xxx.com/xxx/x.jpg'
    return self.compact('query')


def parse(self, p):
    logger = self.logging.getLogger('parse')
    common = self.common
    assert p['vid'], self.message.output('vid')
    vid = p['vid']
    
    mp4 = 'http://xxx.com/xx/x.mp4'
    m3u8 = 'http://xxx.com/xx/x.mp4'
    segs = [{'url':mp4_1},{'url':mp4_2}]
    ext = 'mp4'
    playType = 'm3u8'
    
    ###
    title= 'test'
    duration= 123
    image = 'https://xxx.com/xxx/x.jpg'

    return self.compact('parse')

```
## 打包函数

```    
def compact(self, funcName):
    params = getattr(collect, funcName)(self.params["vtype"])
    locals = sys._getframe(1).f_locals
    inter = set(params).intersection(set(locals.keys()))
    return collect.stream(locals, inter, funcName)
```
