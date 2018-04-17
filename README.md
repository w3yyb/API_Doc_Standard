# API 接口文档规范 API document standard
 
  V1.0
   

 


# 目录 <a name="index"/>
* [一.API接口规范](#api_standard_index)
    * [接口响应规范](#api_resp_index)
    * [接口签名规范](#api_sign_index)
    * [接口请求示例](#api_demo_index)
* [二.API说明](#api_common_index) 
    * [前言](#preface_index)      
    * [非任务推送](#untask_push_index)  
      


# API接口规范 <a name="api_standard_index"/>
## 接口响应规范 <a name="api_resp_index"/>
> HTTP接口遵循API协议规范。返回数据格式统一如下：


```
{
    "code":"", //必选,返回码
    "message":"" ,//可选，返回消息， 
    "other":""可选
    ...
}
```
> Api returnCode定义


code|value
---|---
200|正常
500|其他异常
 


## 接口签名规范 <a name="api_sign_index"/>
>   待写

```php
put php  code here
```
 



# API说明 <a name="api_common_index"/>
 

## 接口1 <a name="untask_push_index"/>
### 应用场景 <a name="yycj_1_index"/>

> 场景1：xxxxxxxx



### XX接口 <a name="UnVarnishedMessage_push_index"/>

描述|内容
---|---
接口功能|功能描述
请求协议|HTTP,HTTPS
请求方法|POST,GET,PUT,DELETE,HEAD,OPTIONS,PATCH.
请求格式|form url encoded,multipart form,file,json,xml...
请求url| http://localhost/pushmsg?name=tom
请求头(和请求格式对应)|Content-Type:application/x-www-form-urlencoded,Content-Type:application/multipart/form-data,Content-Type:application/octet-stream,Content-Type:application/json,Content-Type:application/xml...
备注|可选
请求内容|请求内容
响应码|200
响应头|可选
响应格式|json,xml...


请求参数|如下:

参数|描述|必填|类型
---|---|---|---
param|参数示例1|是|string
param2|参数示例2|是|int


 响应参数|如下:

参数|描述|必有|类型
---|---|---|---
code|响应码|是|int
message|响应消息|否|string
param|参数示例1|否|string
param2|参数示例2|否|int
 
 请求示例：

```
{
    "title": "推送标题",
    "content": "推送内容"
}
```

响应示例：

> 成功情况：

```
{
    "code": "200",
    "message": "成功",
     
}
```

> 失败情况


```
{
    "code": "500",
    "message": "失败",
    
}
```
 

 
