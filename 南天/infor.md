# 日报


王宁9月24日报

```
今日工作：
1. 修改测试报告IDMAP保存文件的问题，合入代码。
2. 修复测试报告问题
3. 
4. 修复FastGPT因为模型切换带来的HTTP 400问题， 协助前端修改慧府右侧朔源信息。
5. 测试验证Agent和多模态功能。


问题反馈：
1. 无

  
解决方案：
1. 无

明日计划：
1. 优化测试报告。
2. 测试验证Agent和多模态功能。
3. 合入代码。

```



网络名称ntxxyd
登录密码Xgcd2825@
网络2号名字：ntxx
密码：Brbcd2825@

8.134.164.50:18080/v1/



wangning2@nantian.com.cn



```bash
docker run --rm -v \
/home/niwang/niwang_proj:/workdir \
pandoc/extra \
-f docx -t pdf /workdir/input.docx -o /workdir/output.pdf \
--pdf-engine=xelatex \
--variable mainfont="SimSun" \
--variable "font-path=/workdir/SimSun.ttf"



docker run -it --rm -v /home/niwang/niwang_proj:/workdir pandoc/latex:latest-ubuntu /bin/bash

docker run -v /home/niwang/niwang_proj:/user/workdir instructure/libreoffice:6.3

docker run -it -v /home/niwang/niwang_proj:/user/workdir instructure/libreoffice:6.3 /bin/bash


```



```
Redhat Linux上word转pdf预到一些困难, 导致RAG报告任务延期。可能要下周一才能看到效果。

问题根因：
1. 本地已经测通过的python word2pdf库，依赖我已经安装好的Office word, linux上只能选择其它方法。
2. Linux上使用宋体（微软商业字体），有报错，我还在尝试。

已经尝试过，但是未成功的方式：
1. LibreOffice， 未购买授权，有水印。


当前进展：
安装Pandoc LateX， 服务器重启中。
```