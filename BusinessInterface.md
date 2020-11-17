# BusinessInterface类

**GetFileFromBusiness()**

参数：无

返回值：文件名和处理字符串

功能描述：轮询业务系统请求，若收到业务系统请求则接收文件到本地，记录审批流程字符串和文件名并返回。

**SubmitReceipt()**

参数：回执文件名

返回值：状态码

功能描述：通过传入的回执文件名向业务系统提交从银行发回的回执，返回提交成功与否的状态码
