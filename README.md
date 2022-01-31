# API 接口文档规范 API document standard
 
  V1.0
   大家有什么意见和建议，可以在issues提出。

 


# 目录 <a name="index"/>
* [一.API接口规范](#api_standard_index)
    * [接口响应规范](#api_resp_index)
    * [接口签名规范](#api_sign_index)
    * [接口请求示例](#api_demo_index)
* [二.API说明](#api_common_index)
    * [接口1](#api_1)
    * [应用场景](#yycj_1_index)


# API接口规范 <a name="api_standard_index"/>
## 接口响应规范 <a name="api_resp_index"/>
> HTTP接口遵循API协议规范。返回数据格式统一如下：


```
{
    "code":"", //必选,返回码
    "message":"" ,//可选，返回消息， 
    "other":""//可选
    ...
}
```
> Api returnCode定义(一般采用http状态码)


code|value
---|---
200|成功
4xx|客户端错误
5xx|服务器端错误
自定义|自定义
 
 http状态码参考 https://httpstatuses.com/


## 接口签名规范 <a name="api_sign_index"/>
>   为了防止提交到接口的明文泄密，可以对提交到接口的数据加密，可以用AES加密算法。微信公众平台官方API接口就是采用此算法。
>   加密方法：所有提交过来的数据都使用AES加密算法+Base64算法加密

1.AES加密参数：

加密模式:AES-128-ECB （可用更安全的aes-128-cbc-微信公众平台在用））

向量iv:空 (aes-128-cbc时需要)

密钥Key：“123456789”(请勿外泄)

填充：PKCS7(PKCS7与PKCS5结果一样)（微信公众平台用的是PKCS7填充）

加密步骤：
对数据进行AES加密。
对AES加密后的数据进行Base64加密。
 

3.加密示例：

1）原始数据：“hello world”

2）AES加密后数据：“bH� �G:9�i_x0005_��”

3）Base64加密后数据：“YkilCuxHOgY5Bv9pGgXcwA==”


```php
<?php
//$key previously generated safely, ie: openssl_random_pseudo_bytes
$key='123456789';
 
  
$plaintext="hello world";
 //$cipher = "aes-128-cbc";
 $cipher = "aes-128-ecb";

if (in_array($cipher, openssl_get_cipher_methods()))
{
     
     
    // $iv='1111111111111111';
    $iv='';
    $ciphertext = openssl_encrypt($plaintext, $cipher, $key, OPENSSL_RAW_DATA, $iv);//如果去掉OPENSSL_RAW_DATA参数,则直接输出base64编码的,不用再base64编码
    $ciphertext =base64_encode($ciphertext);
    //store $cipher, $iv, and $tag for decryption later
    $original_plaintext = openssl_decrypt(base64_decode($ciphertext), $cipher, $key, OPENSSL_RAW_DATA, $iv);


    var_dump( $original_plaintext);
    var_dump( $ciphertext);
}
```
 



# API说明 <a name="api_common_index"/>
 

## 接口1 <a name="api_1"/>
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
响应码|响应码
响应头|可选
响应格式|json,xml...


请求参数,如下:

参数|描述|必填|类型
---|---|---|---
param|参数示例1|是|string
param2|参数示例2|是|int


 响应参数,如下:

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
    "code": 200,
    "message": "成功",
     
}
```

> 失败情况


```
{
    "code": 500,
    "message": "失败",
    
}
```
 

 可参考  ： https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md
