# 数据库设计

## 用户信息表

|  字段   | 名称  |  类型  | 说明  |
|  ----  | ----  |  ----  | ----  |
| 用户ID  |UserID |Long int| 主键 |
| 用户密码|  PWD_Hash  |Var char|     |

## 用户-角色表

|  字段   | 名称  |  类型  | 说明  |
|  ----  | ----  |  ----  | ----  |
| 用户ID  |UserID |Long int| 外键 主键 |
| 角色ID |  CharacterID  |Long int| 主键|

## 业务表

|  字段   | 名称  |  类型  | 说明  |
|  ----  | ----  |  ----  | ----  |
| 请求ID |Require_ID |Long int| 主键 |
| 业务所属角色ID |Role_belong_ID |int| |
| 文件名 |  FIleName  |Var char 1024|
| 优先级 |  Priority  |int|
| 状态   |  Status  |int| 初始、待审批、已审批通过、已审批未通过、已封装、已发送、已确认回执、已提交回业务、异常、已注销|
| 当前审批角色ID |  Approver_ID  |int| 外键|
| 回执文件名 |ReceiptFile |Var char 1024| 默认为空|

## 审批过程表

|  字段   | 名称  |  类型  | 说明  |
|  ----  | ----  |  ----  | ----  |
| 请求ID |Require_ID |Long int| 外键 主键 |
| 审批角色ID |  Approver_ID |Var char 1024| 外键 主键|
| 下一审批角色ID |  Next_approver_ID  |int| 外键|
| 是否审批   |  Finish  |bool| |

# UserInfoDAO

## getPswHash()
### 参数
userID-用户ID
### 返回值
密码的哈希值
### 功能描述
获得密码的哈希值

# RoleInfoDAO

## getRole()
### 参数
userID-用户ID
### 返回值
用户ID对应的所有角色ID
### 功能描述
获得某个用户ID对应的所有角色ID

# BusinessInfoDAO

## addBusiness()
### 参数
业务所属角色ID
### 返回值
请求ID
### 功能描述
向业务表中添加一项新的记录，将状态值设置为0，填入业务所属角色ID，生成请求ID，其余设置为空，最后返回生成的请求ID

## getBusinessID()
### 参数
业务所属角色ID
### 返回值
请求ID的集合
### 功能描述
根据业务所属角色ID查询该角色拥有的业务的记录请求ID，按照业务状态排序后返回

## setFIleName()
### 参数
请求ID 文件名
### 返回值
无
### 功能描述
修改凭据文件名

## setStatus()
### 参数
请求ID 状态值
### 返回值
无
### 功能描述
修改业务记录的状态

## setApproverID()
### 参数
请求ID 角色ID
### 返回值
无
### 功能描述
修改当前审批角色的ID

## setReceiptFile()
### 参数
请求ID 回执文件名
### 返回值
无
### 功能描述
回执文件名

# ApprovalProcessDAO

## addApprovalProcess()
### 参数
请求ID 审批角色ID 下一审批角色ID
### 返回值
无
### 功能描述
审批过程表中添加一条记录，将是否审批字段设置为false

## batchImport()
### 参数
请求ID 审批角色ID序列
### 返回值
无
### 功能描述
调用addApprovalProcess()，根据审批角色ID序列的顺序向审批过程表中添加一系列记录，形成审批顺序的链表

## setApprovalStatus()
### 参数
请求ID 审批角色ID
### 返回值
下一审批角色ID
### 功能描述
修改请求ID和审批角色ID查询到的记录的状态为true，同时返回该记录的下一审批角色ID字段