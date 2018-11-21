项目使用的是MySql存储, 需要先创建以下表结构:

```
CREATE SCHEMA IF NOT EXISTS `alan-oauth` DEFAULT CHARACTER SET utf8 ;
USE `alan-oauth` ;

-- -----------------------------------------------------
-- Table `alan-oauth`.`clientdetails`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `alan-oauth`.`clientdetails` (
  `appId` VARCHAR(128) NOT NULL,
  `resourceIds` VARCHAR(256) NULL DEFAULT NULL,
  `appSecret` VARCHAR(256) NULL DEFAULT NULL,
  `scope` VARCHAR(256) NULL DEFAULT NULL,
  `grantTypes` VARCHAR(256) NULL DEFAULT NULL,
  `redirectUrl` VARCHAR(256) NULL DEFAULT NULL,
  `authorities` VARCHAR(256) NULL DEFAULT NULL,
  `access_token_validity` INT(11) NULL DEFAULT NULL,
  `refresh_token_validity` INT(11) NULL DEFAULT NULL,
  `additionalInformation` VARCHAR(4096) NULL DEFAULT NULL,
  `autoApproveScopes` VARCHAR(256) NULL DEFAULT NULL,
  PRIMARY KEY (`appId`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8;

-- -----------------------------------------------------
-- Table `alan-oauth`.`oauth_access_token`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `alan-oauth`.`oauth_access_token` (
  `token_id` VARCHAR(256) NULL DEFAULT NULL,
  `token` BLOB NULL DEFAULT NULL,
  `authentication_id` VARCHAR(128) NOT NULL,
  `user_name` VARCHAR(256) NULL DEFAULT NULL,
  `client_id` VARCHAR(256) NULL DEFAULT NULL,
  `authentication` BLOB NULL DEFAULT NULL,
  `refresh_token` VARCHAR(256) NULL DEFAULT NULL,
  PRIMARY KEY (`authentication_id`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8;

-- -----------------------------------------------------
-- Table `alan-oauth`.`oauth_approvals`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `alan-oauth`.`oauth_approvals` (
  `userId` VARCHAR(256) NULL DEFAULT NULL,
  `clientId` VARCHAR(256) NULL DEFAULT NULL,
  `scope` VARCHAR(256) NULL DEFAULT NULL,
  `status` VARCHAR(10) NULL DEFAULT NULL,
  `expiresAt` DATETIME NULL DEFAULT NULL,
  `lastModifiedAt` DATETIME NULL DEFAULT NULL)
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8;

-- -----------------------------------------------------
-- Table `alan-oauth`.`oauth_client_details`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `alan-oauth`.`oauth_client_details` (
  `client_id` VARCHAR(128) NOT NULL,
  `resource_ids` VARCHAR(256) NULL DEFAULT NULL,
  `client_secret` VARCHAR(256) NULL DEFAULT NULL,
  `scope` VARCHAR(256) NULL DEFAULT NULL,
  `authorized_grant_types` VARCHAR(256) NULL DEFAULT NULL,
  `web_server_redirect_uri` VARCHAR(256) NULL DEFAULT NULL,
  `authorities` VARCHAR(256) NULL DEFAULT NULL,
  `access_token_validity` INT(11) NULL DEFAULT NULL,
  `refresh_token_validity` INT(11) NULL DEFAULT NULL,
  `additional_information` VARCHAR(4096) NULL DEFAULT NULL,
  `autoapprove` VARCHAR(256) NULL DEFAULT NULL,
  PRIMARY KEY (`client_id`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8;

-- -----------------------------------------------------
-- Table `alan-oauth`.`oauth_client_token`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `alan-oauth`.`oauth_client_token` (
  `token_id` VARCHAR(256) NULL DEFAULT NULL,
  `token` BLOB NULL DEFAULT NULL,
  `authentication_id` VARCHAR(128) NOT NULL,
  `user_name` VARCHAR(256) NULL DEFAULT NULL,
  `client_id` VARCHAR(256) NULL DEFAULT NULL,
  PRIMARY KEY (`authentication_id`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8;

-- -----------------------------------------------------
-- Table `alan-oauth`.`oauth_code`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `alan-oauth`.`oauth_code` (
  `code` VARCHAR(256) NULL DEFAULT NULL,
  `authentication` BLOB NULL DEFAULT NULL)
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8;

-- -----------------------------------------------------
-- Table `alan-oauth`.`oauth_refresh_token`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `alan-oauth`.`oauth_refresh_token` (
  `token_id` VARCHAR(256) NULL DEFAULT NULL,
  `token` BLOB NULL DEFAULT NULL,
  `authentication` BLOB NULL DEFAULT NULL)
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8;
```

要实现四种授权模式，需要先在`oauth_client_details`表中插入4条记录，代表4个客户端，每个客户端代表一种授权模式:
```
INSERT INTO oauth_client_details VALUES ('client', null, 'secret', 'app', 'authorization_code', null, null, null, null, null, null);
INSERT INTO oauth_client_details VALUES ('client_2', null, 'qq', 'all', 'password', null, null, null, null, null, null);
INSERT INTO oauth_client_details VALUES ('client_3', null, 'aa', 'select', 'client_credentials', null, null, null, null, null, null);
INSERT INTO oauth_client_details VALUES ('client_4', null, 'cc', 'read', 'implicit', null, null, null, null, null, null);
```


## 1.Authorization Code Grant:授权码模式

get请求：

http://localhost:8080/oauth/authorize?response_type=code&client_id=client&redirect_uri=https://www.baidu.com

请求此url会提示用户输入用户名和密码，并同意授权，之后重定向到下面的url

https://www.baidu.com/?code=ZDZgEM

获取到授权码后code后需在10s内进行如下操作，一个code只能使用一次

post请求：

http://localhost:8080/oauth/token

参数名称 | 参数值 | 参数说明
---|--- |--- 
grant_type | authorization_code | 授权类型
code | cMTFdj | 授权码
client_id | client | 客户端id
redirect_uri | https://www.baidu.com | 重定向的url
Username | client | 放在Authorization,客户端的用户名
Password | secret | 放在Authorization,客户端的密码
返回示例：
```
{
    "access_token": "17a02bad-9e0c-4a1f-b1bd-41d5dddf52ed",
    "token_type": "bearer",
    "expires_in": 2591999,
    "scope": "app"
}
```

---

## 2.Resource Owner Password Credentials Grant:密码模式：

post请求：

http://localhost:8080/oauth/token

参数名称 | 参数值 | 参数说明
---|--- |--- 
grant_type | password | 授权类型
username | tom | 用户的用户名
password | 123 | 用户的密码
Username | client_2 | 放在Authorization,客户端的用户名
Password | qq | 放在Authorization,客户端的密码
```
响应如下：
{
    "access_token": "393604c8-d2ec-44b8-b3d5-dfd124821d78",
    "token_type": "bearer",
    "expires_in": 2591999,
    "scope": "all"
}
```
---

## 3.Client Credentials Grant:客户端模式：

post请求：

http://localhost:8080/oauth/token

参数名称 | 参数值 | 参数说明
---|--- |--- 
grant_type | client_credentials | 授权类型
Username | client_3 | 放在Authorization,客户端的用户名
Password | aa | 放在Authorization,客户端的密码
```
响应如下：
{
    "access_token": "0b18b42c-19d3-4689-9154-193b26433280",
    "token_type": "bearer",
    "expires_in": 2591992,
    "scope": "select"
}
```
---
## 4.Implicit Grant：简易模式

get请求：

http://localhost:8080/oauth/authorize?response_type=token&client_id=client_4&state=xyz&redirect_uri=https://www.baidu.com

请求此url会提示用户输入用户名和密码，并同意授权，之后重定向到下面的url

https://www.baidu.com/#access_token=813a373f-9b75-4853-a079-45e52742cc60&token_type=bearer&state=xyz%20&expires_in=2591999&scope=read

---
### 说明：

> 通过以上4中方式中的其中一种获取到access_token后，每次请求带上有效的access_token参数，就不会被oauth2拦截，也能得到结果正确的返回结果，若请求参数中无access_token，会被oauth2拦截，并返回如下信息：

```
{
    "error": "unauthorized",
    "error_description": "Full authentication is required to access this resource"
}
```

> 正确的请求示例：http://localhost:8080/hello?access_token=8ddbe594-3c45-4339-a5f8-3e0f5ca103a4

> access_token(令牌)有一定的过期时间，若令牌过期，需重新获取
