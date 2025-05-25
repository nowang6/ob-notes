

NL2SQL基础框架：https://github.com/wbbeyourself/MAC-SQL
评测方法：https://github.com/archerfish-bench/benchmark


- jiesoaping体现， 介绍
- 知识库算法配置方案， 数据端+评测端
- 评估报告内容， 指标和表格
- 如何解读
- 对RAG引擎介绍
- 界面





```
conda create --name hansuo python=3.12.3 -y
conda activate hansuo

nohup uvicorn app.main:app --host 0.0.0.0 --log-config uvicorn_config.json --port 38080 --reload &
```



# prompt


```
As an experienced and professional database administrator, your task is to analyze a user question and a database schema to provide relevant information. The database schema consists of table descriptions, each containing multiple column descriptions. Your goal is to identify the relevant tables and columns based on the user question and evidence provided.


[Instruction]:

1. Discard any table schema that is not related to the user question and evidence.

2. Sort the columns in each relevant table in descending order of relevance and keep the top 6 columns.

3. Ensure that at least 3 tables are included in the final output JSON.

4. The output should be in JSON format.

  

Requirements:

1. If a table has less than or equal to 10 columns, mark it as "keep_all".

2. If a table is completely irrelevant to the user question and evidence, mark it as "drop_all".

3. Prioritize the columns in each relevant table based on their relevance.

  

Here is a typical example:

  

==========

【DB_ID】 banking_system

【Schema】

# Table: account

# Description: account details

[

(account_id, the id of the account. Value examples: [11382, 11362, 2, 1, 2367].),

(district_id, location of branch. Value examples: [77, 76, 2, 1, 39].),

(frequency, frequency of the acount. Value examples: ['POPLATEK MESICNE', 'POPLATEK TYDNE', 'POPLATEK PO OBRATU'].),

(date, the creation date of the account. Value examples: ['1997-12-29', '1997-12-28'].)

]

# Table: client

# Description: client details

[

(client_id, the unique number. Value examples: [13998, 13971, 2, 1, 2839].),

(gender, gender. Value examples: ['M', 'F']. And F：female . M：male ),

(birth_date, birth date. Value examples: ['1987-09-27', '1986-08-13'].),

(district_id, location of branch. Value examples: [77, 76, 2, 1, 39].)

]

# Table: loan

# Description: Details of loans including loan ID, associated account, approval date, amount, duration, payments, and status.

[

(loan_id, the id number identifying the loan data. Value examples: [4959, 4960, 4961].),

(account_id, the id number identifying the account. Value examples: [10, 80, 55, 43].),

(date, the date when the loan is approved. Value examples: ['1998-07-12', '1998-04-19'].),

(amount, the id number identifying the loan data. Value examples: [1567, 7877, 9988].),

(duration, the id number identifying the loan data. Value examples: [60, 48, 24, 12, 36].),

(payments, the id number identifying the loan data. Value examples: [3456, 8972, 9845].),

(status, the id number identifying the loan data. Value examples: ['C', 'A', 'D', 'B'].)

]

# Table: district

# Description: Details of districts including location, area, population, and various socio-economic indicators.

[

(district_id, location of branch. Value examples: [77, 76].),

(A2, area in square kilometers. Value examples: [50.5, 48.9].),

(A4, number of inhabitants. Value examples: [95907, 95616].),

(A5, number of households. Value examples: [35678, 34892].),

(A6, literacy rate. Value examples: [95.6, 92.3, 89.7].),

(A7, number of entrepreneurs. Value examples: [1234, 1456].),

(A8, number of cities. Value examples: [5, 4].),

(A9, number of schools. Value examples: [15, 12, 10].),

(A10, number of hospitals. Value examples: [8, 6, 4].),

(A11, average salary. Value examples: [12541, 11277].),

(A12, poverty rate. Value examples: [12.4, 9.8].),

(A13, unemployment rate. Value examples: [8.2, 7.9].),

(A15, number of crimes. Value examples: [256, 189].)

]

【Foreign keys】

client.`district_id` = district.`district_id`

【Question】

What is the gender of the youngest client who opened account in the lowest average salary branch?

【Evidence】

Later birthdate refers to younger age; A11 refers to average salary

【Answer】

```json

{{

"account": "keep_all",

"client": "keep_all",

"loan": "drop_all",

"district": ["district_id", "A11", "A2", "A4", "A6", "A7"]

}}

```

Question Solved.

  

==========

  

Here is a new example, please start answering:

  

【DB_ID】 {db_id}

【Schema】

{desc_str}

【Foreign keys】

{fk_str}

【Question】

{query}

【Evidence】

{evidence}

【Answer】

"""
```