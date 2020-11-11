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

## getBusinessID()