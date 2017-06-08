## 华瑞银行开放平台API接口接入说明

#### 文档版本号
> V1.0  20170410  正式版发布，调整接口字段说明

#### 接入安全控制

* VPN

* HTTPS双向认证

  为保证HTTPS通讯安全，使用双向HTTPS认证，接入方HTTPS证书由权威第三方CA签发。

* 报文数据签名

  原始数据:

  ```json
  {
    "appAuthToken": "value",
    "appID": "value",
    "encryptMethod": "NONE",
    "reqData": {
        "appNo": "A000001"
    },
    "sequenceID": "123456",
    "sign": "value",
    "signMethod": "MD5"
  }
  ```

  首先取出`reqData`里的所有数据，包括'{'和'}'

  ```json
  {
    "appNo": "A000001"
  }
  ```

  然后拼接上`sequenceID`获得待签名的字符串

  ```json
  {"appNo": "A000001"}123456
  ```

  签名算法支持HASH和RSA两类,对于RSA类签名算法，直接使用开发者私钥进行加签。
  对于HASH类签名算法，还需要在待签名字符串之后拼接上`appSecret`的值。
  
  > 在开放平台申请应用之后，每个应用都会有唯一的`appID`和`appSecret`
  
  ```
  {"appNo": "A000001"}123456appSecret
  ```

  使用HASH算法对上面的待签名字符串进行签名，最后将签名得到的结果放入`sign`字段上传。
    
  > HASH类算法支持MD5、SHA1、SHA256、SHA512
  
  服务端返回的数据采用同样的算法对`rspData`进行签名。
  
* 报文数据加密

  如果开发者开通了报文加密功能，请求时直接对`reqData`里的所有数据进行加密，包括'{'和'}'

  <table><tr><td bgcolor=#FFEBCD><b>注意</b>：发送请求时先加密再加签，接收请求时先验签再解密</td></tr></table>
  
  原始数据:

  ```json
  {
    "appAuthToken": "value",
    "appID": "value",
    "encryptMethod": "NONE",
    "reqData": {
        "appNo": "A000001"
    },
    "sequenceID": "123456",
    "sign": "value",
    "signMethod": "MD5"
  }
  ```

  加密后数据:

  ```json
  {
    "appAuthToken": "value",
    "appID": "value",
    "encryptMethod": "NONE",
    "reqData": "加密后数据变为json普通元素",
    "sequenceID": "123456",
    "sign": "value",
    "signMethod": "MD5"
  }
  ```

  服务器同样会对`rspData`内的所有返回数据进行加密，加密算法一般采用AES。
  
![](/assets/接入安全.png)

