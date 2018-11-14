# 开放平台接口文档
## 测试环境地址
### http://127.0.0.1:8080/open-admin

---

## （普通用户）的主要功能
### 1.  我的应用 - 应用列表
- 请求URL:

```
 /myapp/list
```
- 请求方式:
-  GET
- 参数:

参数名 | 必选 | 类型 | 说明
---|---|---|---
page|否|Integer|当前页
limit|否|Integer|每页条数
- 返回实例
```
{
    "msg": "success",
    "code": 0,
    "page": {
        "totalCount": 1,
        "pageSize": 10,
        "totalPage": 1,
        "currPage": 1,
        "list": [
            {
                "id": 1,
                "userId": 1,
                "productCode": "12",
                "appId": "234",
                "name": "测试应用",
                "code": "code",
                "appSecret": "secret",
                "createTime": "2018-11-02 20:10:31",
                "updateTime": "2018-11-02 20:10:31"
            }
        ]
    }
}
```
- 备注:更多返回错误代码请看首页的错误代码描述

---

### 2.  我的应用 - 创建应用
- 请求URL:

```
 /myapp/create
```
- 请求方式:
-  POST
- 参数:

参数名 | 必选 | 类型 | 说明
---|---|---|---
productCode|是|String|产品代码
appId|是|String|应用ID
name|是|String|应用名称
code|是|String|应用代码
appSecret|是|String|应用Secret
- 返回实例
```
{
    "msg": "success",
    "code": 0
}
```
- 备注:更多返回错误代码请看首页的错误代码描述

---
### 3.  我的应用 - 更新app secret
- 请求URL:

```
 /myapp/updatesecret
```
- 请求方式:
-  POST
- 参数:

参数名 | 必选 | 类型 | 说明
---|---|---|---
appId|是|String|应用ID
appSecret|是|String|应用Secret
- 返回实例
```
{
    "msg": "success",
    "code": 0
}
```
- 备注:更多返回错误代码请看首页的错误代码描述
---
### 4.  我的账户 - 余额查询
- 请求URL:

```
 /myaccount/balance
```
- 请求方式:
-  GET
- 参数:

参数名 | 必选 | 类型 | 说明
---|---|---|---
- 返回实例
```
{
    "msg": "success",
    "customerWalletEntity": {
        "id": 3,
        "userId": 1,
        "amount": 1623,
        "createTime": "2018-11-03 14:52:42",
        "updateTime": "2018-11-06 20:42:15"
    },
    "code": 0
}
```
- 备注:更多返回错误代码请看首页的错误代码描述
---
### 5.  我的账户 - 充值记录
- 请求URL:

```
 /myaccount/recharge
```
- 请求方式:
-  GET
- 参数:

参数名 | 必选 | 类型 | 说明
---|---|---|---
page|否|Integer|当前页
limit|否|Integer|每页条数
- 返回实例
```
{
    "msg": "success",
    "code": 0,
    "page": {
        "totalCount": 2,
        "pageSize": 10,
        "totalPage": 1,
        "currPage": 1,
        "list": [
            {
                "id": 3,
                "userId": 1,
                "type": 1,
                "amount": 123,
                "productCode": "tjggy",
                "appId": "43453",
                "createTime": "2018-11-06 20:42:12",
                "updateTime": "2018-11-06 20:42:13"
            },
            {
                "id": 2,
                "userId": 1,
                "type": 1,
                "amount": 1500,
                "productCode": "rtre",
                "appId": "放电饭锅",
                "createTime": "2018-11-03 14:52:28",
                "updateTime": "2018-11-03 14:52:36"
            }
        ]
    }
}
```
- 备注:更多返回错误代码请看首页的错误代码描述
---
### 6.  我的账户 - 扣费记录
- 请求URL:

```
 /myaccount/charging
```
- 请求方式:
-  GET
- 参数:

参数名 | 必选 | 类型 | 说明
---|---|---|---
page|否|Integer|当前页
limit|否|Integer|每页条数
- 返回实例
```
{
    "msg": "success",
    "code": 0,
    "page": {
        "totalCount": 0,
        "pageSize": 10,
        "totalPage": 0,
        "currPage": 1,
        "list": []
    }
}
```
- 备注:更多返回错误代码请看首页的错误代码描述
---
### 7.  我的账户 - 新增充值
- 请求URL:

```
 /myaccount/addrecharge
```
- 请求方式:
-  POST
- 参数:

参数名 | 必选 | 类型 | 说明
---|---|---|---
amount|是|Integer|充值金额
productCode|是|String|产品代码
appId|是|String|应用ID
- 返回实例
```
{
    "msg": "success",
    "code": 0
}
```
- 备注:更多返回错误代码请看首页的错误代码描述
    



    
