# 环境

```sh
apt install mpich libmpich-dev
```

```sh
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
pip config set global.index-url https://pypi.mirrors.ustc.edu.cn/simple/
conda create --name hansuo python=3.12 -y
conda activate hansuo

```

```python
jupyter lab --ip='*' --port=8080 --notebook-dir='/home/niwang/jupter' --no-browser

```

```python
import os

# 设置代理地址和端口号
proxy_address = "127.0.0.1"
proxy_port = "7890"

# 设置HTTP代理
os.environ["HTTP_PROXY"] = f"http://{proxy_address}:{proxy_port}"
os.environ["HTTPS_PROXY"] = f"http://{proxy_address}:{proxy_port}"

# 可选：设置FTP代理
os.environ["FTP_PROXY"] = f"ftp://{proxy_address}:{proxy_port}"

# 可选：设置SOCKS代理
os.environ["SOCKS_PROXY"] = f"socks://{proxy_address}:{proxy_port}"

```



# 基础

## Iterators and Iterables
[Python 迭代器(Iterators and Iterables) - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/527777736)

## Map函数

``` python
def chen(x:int, y:int):
    return x*y
a = (1,2,3,4,5)
b = (1,2,3,4,5)
c = list(map(chen,a,b))

print (c)
```

## Filter 函数

```Python
def is_double(x:int):
    return x%2 == 0
a = (1,2,3,4,5)
c = list(filter(is_double,a))
print (c)
```

## Reduce 函数
```Python
from functools import reduce

a = [1, 2, 3, 4, 5]

def add(x, y):
    return x + y
print(reduce(add, a))
```

## 参数解析
```python
import argparse
parser = argparse.ArgumentParser()
parser.add_argument('--bert_path', help='config file', default='/home/data/tmp/bert-base-chinese')
args = parser.parse_args()
args.bert_path
```

## 闭包和装饰器

```
在函数嵌套（函数里面再定义函数）的前提下
内部函数使用了外部函数的变量（参数）
外部函数的返回值是内部函数的引用
```

装饰器是一种闭包


## Pytest

**（1）.py测试文件必须以“test_”开头（或“_test”结尾）**

**（2）测试类必须以Test开头，并且不能有init方法**

**（3）测试方法必须以“test_”开头**

（4）断言必须使用assert**



# Debug

python -m pdb linked-list-cycle.py

```
n  #执行下一行
b 33 #第33行插入短点
c  #执行到断点
s  #进入函数
bt #查看函数调用链
p 变量名 #输出变量值

where 当前的调用stack
up 跳到上面一个调用stack
down 进入下面一个调用stack

help
help (up) 查看help的帮助文档
```



|命令|解释|
|---|---|
|break 或 b 设置断点|设置断点|
|continue 或 c|继续执行程序|
|list 或 l|查看当前行的代码段|
|step 或 s|进入函数|
|return 或 r|执行代码直到从当前函数返回|
|exit 或 q|中止并退出|
|next 或 n|执行下一行|
|pp|打印变量的值|
|help|帮助|


# Pandas

传ArrayLik ,  是竖起来的
```python
s = pd.Series(list("abc"))  
df = pd.DataFrame(s)

   0
0  a
1  b
2  c

```
传Series列表，是躺着的
```python
s = pd.Series(list("abc"))  
df = pd.DataFrame([s,s])

   0  1  2
0  a  b  c
1  a  b  c
```


# Jupter
```bash
pip install jupyterlab

nohup jupyter lab --ip 0.0.0.0 --port 8080 &
```

# PDF解析

![[Pasted image 20240208180623.png]]

七月：sciencebeam

## Sci PDF
环境准备
```bash
docker run --rm --gpus all --init --ulimit core=0 -p 8070:8070 grobid/grobid:0.7.3
```

解析

```python
pdf_file = ''
trg_path = "target"

article_dict = scipdf.parse_pdf_to_dict(str(pdf_file)) # return dictionary
with open(trg_path, "w") as f:
	json.dump(article_dict, f, ensure_ascii=False)
```



# 并发编程
## 并发 vs  并行
并发：同一时刻，只有一个thread/task执行，thread对应threading库， task对应asyncio库， 应用于I/O操作频繁的场景， 比如爬虫。

并行：使用multi-processing启动多个进程，应用于CPU heavy的场景。

### 使用原则
如果是I/O bound，并且I/O操作很慢，需要很多任务/线程协同实现，那么使用Asyncio更合适。

如果是I/O bound，但是I/O操作很快，只需要有限数量的任务/线程，那么使用多线程Threading就可以了。

如果是CPU bound，则需要使用多进程来提高程序运行效率


# Pytorch 


## Variable（变量）
variable(废弃)是封装了tensor并提供自动求导功能的对象
```python
from torch.autograd import Variable

```

# Flash Attention
```sh
git clone https://github.com/Dao-AILab/flash-attention
cd flash-attention
python setup.py install
cd csrc/rotary && pip install .
```


# 扩展参数


```python
args = [
        '--model_name', 'deepseek-coder',
        '--data_path', 'https://github.com/SWE-agent/test-repo/issues/1',
        '--config_file', 'config/default_from_url.yaml',
        '--per_instance_cost_limit', '2.00',
        
    ]
sys.argv.extend(args)

```



# 暴露环境


nohup ngrok http 8080 --log=stdout > ngrok.log &





左老师，下午有时间了对一下
1. 需求的优先级，做哪些需求。
2. 责任人和工作量评估。
3. 计划。