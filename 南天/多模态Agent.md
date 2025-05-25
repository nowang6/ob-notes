
![[Pasted image 20240903103337.png]]






# 创建接口

```sql
INSERT INTO ntcgpt_knowldege_cusvr(
						cusvr_name,
						cusvr_base_id,
						cusvr_desc,
						owner,
						created_at,
						cusvr_status,
						cusvr_base_type,
						param1,
						param2,
						cusvr_tools,
						cusvr_knowldege_bases
					)
					VALUES(
						#{p.cusvrName},
						#{p.cusvrBaseId},
						#{p.cusvrDesc},
						#{myid},
						#{time1},
						3,
						#{cusvrBaseType},
						#{param1},
						#{param2},
						#{p.cusvrTools},
						#{p.cusvrKnowldegeBases}
					); 
```


![[Pasted image 20240903104856.png]]

```json
http://101.200.222.48:18100/ntcgpt/service/ant/dao/addKnowldegeCusvr

{
   "cusvrName":"x'x'x",
   "cusvrBaseId":"1000427",
   "setDesc":"xxx",
   "reDesc":"xxx",
   "cusvrBaseType":"RAG",
   "cusvrDesc":" "
}

```


# 修改数据库
修改ntcgpt_knowldege_cusvr， 增加2个字段
```sql
ALTER TABLE ntcgptdb.ntcgpt_knowldege_cusvr cusvr_tools varchar(255) NULL COMMENT '工具列表，以逗号分隔';
ALTER TABLE ntcgptdb.ntcgpt_knowldege_cusvr cusvr_memories varchar(255) NULL COMMENT '知识库列表, 以逗号分隔';
ALTER TABLE ntcgptdb.ntcgpt_knowldege_cusvr ADD cusvr_llm varchar(100) NULL COMMENT 'agent的模型';

ALTER TABLE ntcgptdb.ntcgpt_knowldege_cusvr ADD cusvr_knowldege_bases varchar(255) NULL COMMENT '知识库列表, 以逗号分隔，来自于ntcgpt_knowldege_base主键';

ALTER TABLE ntcgptdb.ntcgpt_knowldege_cusvr ADD cusvr_llm varchar(100) NULL COMMENT 'agent的模型';
```



# 工具


```json
 {
        "type": "function",
        "function": {
            "name": "search_image",
            "description": "用一个关键字搜索图片",
            "parameters": {
                "type": "object",
                "properties": {
                    "keyword": {
                        "type": "string",
                        "description": "用于搜索图片的关键字。 比如：南天落地方案",
                    }
                },
                "required": ["keyword"],
            },
        }
    },
    {
        "type": "function",
        "function": {
            "name": "image_generation",
            "description": "使用一个指令生成一张图片",
            "parameters": {
                "type": "object",
                "properties": {
                    "prompt": {
                        "type": "string",
                        "description": "用于生成图片的指令, 比如：请生成一只可爱的猫",
                    }
                },
                "required": ["prompt"]
            },
        }
    },
     {
        "type": "function",
        "function": {
            "name": "descripe_image",
            "description": "描述一张图片",
            "parameters": {
                "type": "object",
                "properties": {
                    "image_uri": {
                        "type": "string",
                        "description": "这张图片的URI地址，比如： https://example.com/image.jpg",
                    },
                    "question": {
                        "type": "string",
                        "description": "针对图片的提问，比如： 请描述图片",
                    },
                },
                "required": ["image_uri","question"]
            },
        }
    },
    {
        "type": "function",
        "function": {
            "name": "other_functions",
            "description": "不属于以上的函数",
            "parameters": {
                "type": "object",
                "properties": {
                    "prompt": {
                        "type": "string",
                        "description": "用户的原始指令或者问题，比如： 南天是什么时候成立的？",
                    }
                },
                "required": ["prompt"]
            },
        }
    },
```








# 环境


```
python -m vllm.entrypoints.openai.api_server \
--model /home/niwang/models/Qwen2-7B-Instruct \
--max-model-len 8192

```




```
Moonshot-v1-32k: 长文本，便宜
Moonshot-v1-128k:  长文本，便宜
Gemini 1.0 Pro: 效果好 （需要科学上网）
Claude 3.5: 效果好 （需要科学上网）
```

