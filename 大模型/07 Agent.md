

```bash
python run.py \
--model_name deepseek-coder \
--data_path https://github.com/SWE-agent/test-repo/issues/1 \
--config_file config/default_from_url.yaml \
--per_instance_cost_limit 2.00
```





# 数据

MSAgent-Bench

![[Pasted image 20240909135716.png]]




# 项目


AutoGPT

MetaGPT





9月27日 《王佳Agent交流》记录
时间：14：00 ~14：40
参与人：王宁， 王佳

王佳看到一些客户已经基于FastGPT/Dify开始做工作流和Agent, 广州团队考虑做Agent,  如何跟成都团队配合？另外广州团队技术比较传统，主要是Java/VUE JS

王宁在慧府里给王佳展示了Agent，主要原理是ReACT Agent。
王宁建议广州团队围绕客户化工具和场景，成都团队围绕大模型的COT能力和公共工具，大家都采用langchain的工具定义格式，这样工具可以互通。

王佳询问，现在有新员工培训的场景应该如何实现?  王宁基于以前项目经验，给王佳展示如何使用FastGPT工作流定义一个新员工培训机器人。

王宁给王佳分析了FastGPT和Dify的技术和优缺点。


