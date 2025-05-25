

- jiesoaping体现， 介绍评价体系
- 知识库算法配置方案， 数据端+评测端
- 评估报告内容， 指标和表格
- 如何解读
- 对RAG引擎介绍
- 界面






```
eval_id: 1000489
ntcgpt_raga_project


base_id: 1000548
ntcgpt_knowldege_trains


ntcgpt_rag_data_ex
ntcgpt_rag_data_ex
ntcgpt_rag_data
```



```sql
ntcgpt_raga_project


SELECT

benchmark_id,

base_id,

search_opt

from

ntcgpt_raga_project

where

eva_prj_id = '1000513';
```



```sql
ntcgpt_rag_bencemark

select evaluation_name from ntcgpt_rag_bencemark where ntcgpt_rag_bencemark.evaluation_id ='1000078';
```



```sql

SELECT

base_id,

kno_train_name,

kno_train_desc,

text_handle,

text_cut,

embedding,

vector_index_type,

search_opt,

rag_train_id

from

ntcgpt_knowldege_trains

where

kno_train_id = '1000560';
```




flatpak run org.libreoffice.LibreOffice --headless --convert-to pdf --outdir /root/niwang-proj/raga-report /root/niwang-proj/raga-report/数币RAG-bge1.5-更新测评数据3-new-1000501.docx   



flatpak run org.libreoffice.LibreOffice  /root/niwang-proj/raga-report/input.docx

flatpak run org.libreoffice.LibreOffice --headless --convert-to pdf --outdir /home/ntcgpt/dev-restful/raga-report /home/ntcgpt/dev-restful/raga-report/数币RAG-bge1.5-更新测评数据3-new-1000501.docx



```js
<button @click="downloadPDF">下载PDF报告</button>


async generatePDFReport() {

var data = {

evaId: this.$route.query.evaId,

};

const evaId = this.$route.query.evaId;

await getRagReportPDF(data)

.then((res) => {

const data = response.data;

  

// 使用 jsPDF 生成 PDF

const { jsPDF } = window.jspdf;

const doc = new jsPDF();

  

// 添加内容到 PDF

doc.text("Report Title", 10, 10);

doc.text(`Data: ${data}`, 10, 20);

  

// 下载 PDF

doc.save('report.pdf');

})

},

云南南天电子信息产业股份有限公司

/ntcgpt/service/ant/dao/ntcgptRagaReportPDF
/ntcgpt/service/ant/dao/ntcgptRagaReportPDF

```