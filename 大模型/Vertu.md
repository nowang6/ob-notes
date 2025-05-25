
VERTU AI知识库
https://lib.vertu.cn/account
wangning


xhjy1111



export https_proxy=http://101.200.222.48:7890 http_proxy=http://101.200.222.48:7890 all_proxy=socks5://101.200.222.48:7890


```
[Service] 
Environment="HTTP_PROXY=http://101.200.222.48:7890" Environment="HTTPS_PROXY=http://101.200.222.48:7890" Environment="NO_PROXY=localhost,127.0.0.1"
```