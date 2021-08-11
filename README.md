#  API 文档
##### version __1.0.0__
##### 内网接口地址 http://120.79.187.219:8080

<br>
### I ChangeLog

  - 2019-3-19
    - 初始化

### II 约定


- 请求报文：
  - appId:APP标识 第一个固定为1
  - channel:渠道字段苹果固定为"iOS" 安卓对应渠道打包
  - sign:data字段的签名
  - v:版本号 每个APP的初始值为1
  - token:登录标识
  - data:json类型  所有的入参都放里面
  - data.timestamp:时间戳 每次请求都要传(设备本地的当前时间戳)
```json
{
  "appId": 1,  
  "channel": "iOS",  
  "v": 1,  
  "token": "8edb3d300e754bad9d0e97da6d6c781e",  
  "sign": "8edb3d300e754bad9d0e97da6d6c781e",
  "data": "{'timestamp':'524357435743574'}"
}
```


- 返回报文：
  - code: 返回的状态码 全局的状态码(0 成功 1失败 33登录过期(跳转至登录页面) 55 验签失败)
  - message:提示信息(如果失败终端直接用后端返回的提示信息)
  - timestamp: 时间戳
  - data:json类型  所有的出参都在里面
```json
{
  "code": 0,
  "message": "成功",
  "timestamp": 524357435743574,
  "data": "{}"
}
```

### III 静态页面地址
- 帮助中心：http://120.79.187.219:8080/html/question.html?app=1
- 用户协议：http://120.79.187.219:8080/html/serviceProvision.html?app=1
- 商务合作：http://120.79.187.219:8080/html/cooperation.html?app=1

### III 目录
- [x] 1.[页面相关](#1页面相关)
  - [x] [1.1 首页](#11-首页)
  - [x] [1.2 产品列表](#12-产品列表)
  - [x] [1.3 产品详情](#13-产品详情)
  - [x] [1.4 点击记录列表](#14-点击记录列表)
  - [x] [1.5 贷款列表处的借款类型](#15-贷款列表处的借款类型)
  - [x] [1.6 ab面切换](#16-ab面切换)
- [x] 2.[验证码相关](#2验证码相关)
  - [x] [2.1 短信验证码登录验证码](#21-短信验证码登录验证码)
  - [x] [2.2 忘记密码验证码](#22-忘记密码验证码)
  - [x] [2.3 图形验证码](#23-图形验证码)
- [x] 3.[用户相关](#3用户相关)
  - [x] [3.1 验证码登录](#31-验证码登录)
  - [x] [3.2 密码登录](#32-密码登录)
  - [x] [3.3 忘记密码](#33-忘记密码)
  - [x] [3.4 新增点击记录](#34-新增点击记录)



------

### 1.页面信息

#### 1.1 首页
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/page/indexPage.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>获取首页数据</td>
    </tr>
  </tbody>
</table>

##### data入参
无

##### data出参

参数名|非空|类型|说明
---|---|---|---
bannerList | 是 | List| banner数组
bannerList.title | 是 | String| 标题(跳转外链的时候,顶部用这个字段)
bannerList.imgUrl | 是 | String| 图片地址
bannerList.type | 是 | int| 1 内链产品详情 2外链打开链接 3 产品列表
bannerList.productId | 是 | int| 产品ID
bannerList.url | 是 | String| 外链地址
bannerList.listImgUrl | 是 | String| 列表图片地址  (为空得话就隐藏顶部得图片)
bannerList.listUrl | 是 | String| 列表图片点击链接地址  (为空得话就没有点击事件)
bannerList.listType | 是 | String| 列表类型(用于产品列表得中的listType入参)
informationsList | 是 | List| 轮播数组
informationsList.content | 是 | String| 轮播内容
informationsList.productId | 是 | int| 产品ID
typeList | 是 | List| 类型数组
typeList.name | 是 | String| 类型名字
typeList.typeId | 是 | int| 类型ID
typeId.listImgUrl | 是 | String| 列表图片地址  (为空得话就隐藏顶部得图片)
typeId.listUrl | 是 | String| 列表图片点击链接地址  (为空得话就没有点击事件)
typeId.listType | 是 | String| 列表类型(用于产品列表得中的listType入参)
jrtjList | 是 | List| banner数组
jrtjList.name | 是 | String| 产品名
jrtjList.imgUrl | 是 | String| 图片地址
jrtjList.adver | 是 | String| 广告语
jrtjList.productId | 是 | int| 产品ID
jrtjList.moneyMax | 是 | int| 最大金额
jrtjList.moneyMin | 是 | int| 最小金额
jrtjList.rateMin | 是 | int| 最低利率
jrtjList.rateType | 是 | int| 利率类型
jrtjList.loanNum | 是 | int| 申请数(也是下款数)
rmList | 是 | List| banner数组
rmList.name | 是 | String| 产品名
rmList.imgUrl | 是 | String| 图片地址
rmList.adver | 是 | String| 广告语
rmList.productId | 是 | int| 产品ID
rmList.label | 是 | String| 标签文本
rmList.moneyMax | 是 | int| 最大金额
rmList.moneyMin | 是 | int| 最小金额
rmList.rateMin | 是 | int| 最低利率
rmList.rateType | 是 | int| 利率类型
rmList.loanNum | 是 | int| 申请数(也是下款数)

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
    "bannerList": [
      {
        "title": "banner",
        "imgUrl": "http://hyj-pro.oss-cn-shenzhen.aliyuncs.com//banner/img/1546597345872.jpg",
        "type": 1,
        "productId": 1,
        "url": "http://www.baidu.com",
		"listImgUrl": "http://hyj-pro.oss-cn-shenzhen.aliyuncs.com//banner/img/1546597345872.jpg",
		"listUrl": "http://www.baidu.com",
		"listType": 1
      },
      {
        "title": "banner",
        "imgUrl": "http://hyj-pro.oss-cn-shenzhen.aliyuncs.com//banner/img/1546597345872.jpg",
        "type": 2,
        "productId": 1,
        "url": "http://www.baidu.com",
		"listImgUrl": "http://hyj-pro.oss-cn-shenzhen.aliyuncs.com//banner/img/1546597345872.jpg",
		"listUrl": "http://www.baidu.com",
		"listType": 1
      }
    ],
    "informationsList": [
      {
        "content": "轮播内容1",
        "productId": 1
      },
      {
        "content": "轮播内容2",
        "productId": 2
      }
    ],
    "typeList": [
      {
        "name": "学生贷",
        "typeId": 1,
		"listImgUrl": "http://hyj-pro.oss-cn-shenzhen.aliyuncs.com//banner/img/1546597345872.jpg",
		"listUrl": "http://www.baidu.com",
		"listType": 1
      },
      {
        "name": "工薪贷",
        "typeId": 2,
		"listImgUrl": "http://hyj-pro.oss-cn-shenzhen.aliyuncs.com//banner/img/1546597345872.jpg",
		"listUrl": "http://www.baidu.com",
		"listType": 1
      },
      {
        "name": "企业贷",
        "typeId": 3,
		"listImgUrl": "http://hyj-pro.oss-cn-shenzhen.aliyuncs.com//banner/img/1546597345872.jpg",
		"listUrl": "http://www.baidu.com",
		"listType": 1
      }
    ],
    "jrtjList": [
      {
        "name": "产品名1",
        "productId": 1,
        "imgUrl": "http://hyj-pro.oss-cn-shenzhen.aliyuncs.com//product/logo/1551449524295.jpg",
        "adver": "广告语",
		"moneyMax": 111,
		"moneyMin": 1,
		"rateMin": 0.2,
		"rateType": 1,
		"loanNum": 12345
      },
      {
        "name": "产品名2",
        "productId": 2,
        "imgUrl": "http://hyj-pro.oss-cn-shenzhen.aliyuncs.com//product/logo/1551449524295.jpg",
        "adver": "广告语",
		"moneyMax": 111,
		"moneyMin": 1,
		"rateMin": 0.2,
		"rateType": 1,
		"loanNum": 12345
      },
      {
        "name": "产品名3",
        "productId": 3,
        "imgUrl": "http://hyj-pro.oss-cn-shenzhen.aliyuncs.com//product/logo/1551449524295.jpg",
        "adver": "广告语",
		"moneyMax": 111,
		"moneyMin": 1,
		"rateMin": 0.2,
		"rateType": 1,
		"loanNum": 12345
      },
      {
        "name": "产品名4",
        "productId": 4,
        "imgUrl": "http://hyj-pro.oss-cn-shenzhen.aliyuncs.com//product/logo/1551449524295.jpg",
        "adver": "广告语",
		"moneyMax": 111,
		"moneyMin": 1,
		"rateMin": 0.2,
		"rateType": 1,
		"loanNum": 12345
      }
    ],
    "rmList": [
      {
        "name": "产品名1",
        "productId": 1,
        "imgUrl": "http://hyj-pro.oss-cn-shenzhen.aliyuncs.com//product/logo/1551449524295.jpg",
        "adver": "广告语",
        "label": "热门",
		"moneyMax": 111,
		"moneyMin": 1,
		"rateMin": 0.2,
		"rateType": 1,
		"loanNum": 12345
      },
      {
        "name": "产品名2",
        "productId": 2,
        "imgUrl": "http://hyj-pro.oss-cn-shenzhen.aliyuncs.com//product/logo/1551449524295.jpg",
        "adver": "广告语",
        "label": "",
		"moneyMax": 111,
		"moneyMin": 1,
		"rateMin": 0.2,
		"rateType": 1,
		"loanNum": 12345
      },
      {
        "name": "产品名3",
        "productId": 3,
        "imgUrl": "http://hyj-pro.oss-cn-shenzhen.aliyuncs.com//product/logo/1551449524295.jpg",
        "adver": "广告语",
        "label": "热门",
		"moneyMax": 111,
		"moneyMin": 1,
		"rateMin": 0.2,
		"rateType": 1,
		"loanNum": 12345
      },
      {
        "name": "产品名4",
        "productId": 4,
        "imgUrl": "http://hyj-pro.oss-cn-shenzhen.aliyuncs.com//product/logo/1551449524295.jpg",
        "adver": "广告语",
        "label": "",
		"moneyMax": 111,
		"moneyMin": 1,
		"rateMin": 0.2,
		"rateType": 1,
		"loanNum": 12345
      }
    ]
  },
  "timestamp": 1552992853177
}
```
------


#### 1.2 产品列表
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/page/productListPage.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>产品列表</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
pageNum | 是 | int | 页数从1开始
pageSize | 是 | int | 每页多少条 暂定10条
moneyMin | 是 | int | 最小金额(0为不限制最小)
moneyMax | 是 | int | 最大金额(0为不限制最大)
typeId | 是 | int | 类型ID 0为全部
sort | 是 | int | 排序 0 默认排序 1 成功率高 2 利率低 3 额度高 4放款快
bannerId | 是 | int | banner点击跳转列表的时候
listType | 是 | int | 列表类型(banner或者类型点击的时候传对应的值),没有就默认传0

##### 出参

参数名|非空|类型|说明
---|---|---|---
dataList | 是 | String | 产品数组
dataList.name | 是 | String | 产品名
dataList.productId | 是 | String | 产品ID
dataList.imgUrl | 是 | String | 产品logo
dataList.adver | 是 | String | 广告语
dataList.moneyMax | 是 | String | 最小金额
dataList.rateMin | 是 | String | 最低利率  直接后面加%
dataList.rateType | 是 | String | 利率类型 1 日利率 2 月利率  
dataList.success | 是 | String | 成功率 直接再后面加%
dataList.loanNum | 是 | String | 下款人数(申请人数)
dataList.label | 是 | String | 标签文本
dataCount | 是 | String | 数据总数(用于分页)

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
    "dataList": [
      {
        "name": "产品名1",
        "productId": 1,
        "imgUrl": "http://hyj-pro.oss-cn-shenzhen.aliyuncs.com//product/logo/1551449524295.jpg",
        "adver": "广告语",
        "moneyMax": 100000,
		"loanNum": 100000,
        "rateMin": 0.02,
        "rateType": 1,
        "success": 88,
        "label": "热门"
      },
      {
        "name": "产品名2",
        "productId": 2,
        "imgUrl": "http://hyj-pro.oss-cn-shenzhen.aliyuncs.com//product/logo/1551449524295.jpg",
        "adver": "广告语",
        "moneyMax": 100000,
		"loanNum": 100000,
        "rateMin": 0.02,
        "rateType": 1,
        "success": 88,
        "label": ""
      }
    ],
    "dataCount": 2
  },
  "timestamp": 1552993913106
}
```
------

#### 1.3 产品详情
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/page/productInfoPage.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>产品详情</td>
    </tr>
  </tbody>
</table>

##### data入参
参数名|非空|类型|说明
---|---|---|---
productId | 是 | int| 产品ID

##### 出参

参数名|非空|类型|说明
---|---|---|---
productId | 是 | int| 产品ID
rateType | 是 | int | 利率类型 1 日利率 2 月利率  
name | 是 | String | 产品名
moneyMin | 是 | int | 最小金额 单位元(注意千万转化)
moneyMax | 是 | int | 最大金额 单位元(注意千万转化)
dayMin | 是 | int | 最小天数 注意月年转化
dayMax | 是 | int | 最大天数 注意月年转化
rateMin | 是 | double | 最小利率 直接加%
rateMax | 是 | double | 最大利率 直接加%
loanTime | 是 | int | 下款时间  单位分钟 注意小时转化
success | 是 | double | 成功率 直接再后面加%
loanNum | 是 | int | 下款人数 不用转化  直接显示出来
adver | 是 | String | 广告语
applicationConditions | 是 | String | 申请条件
requiredMaterials | 是 | String | 所需材料
applicationProcess | 是 | String | 申请流程
imgUrl | 是 | String | 图片地址
url | 是 | String | 申请地址



sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
    "productId": 1,
    "rateType": 1,
    "name": "产品名1",
    "moneyMin": 100,
    "moneyMax": 100000,
    "dayMin": 7,
    "dayMax": 360,
    "rateMin": 0.02,
    "rateMax": 0.03,
    "loanTime": 5,
    "success": 88,
    "loanNum": 435345,
    "adver": "广告语",
    "applicationConditions": "申请条件",
    "requiredMaterials": "所需材料",
    "applicationProcess": "申请条件",
    "imgUrl": "http://hyj-pro.oss-cn-shenzhen.aliyuncs.com//product/logo/1551449524295.jpg",
    "url": "http://www.baidu.com"
  },
  "timestamp": 1552994174264
}
```

------

#### 1.4 点击记录列表
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/page/loanRecordListPage.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>点击记录列表</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
pageNum | 是 | int | 页数从1开始
pageSize | 是 | int | 每页多少条 暂定10条

##### 出参

参数名|非空|类型|说明
---|---|---|---
dataList | 是 | String | 产品数组
dataList.name | 是 | String | 产品名
dataList.productId | 是 | String | 产品ID
dataList.imgUrl | 是 | String | 产品logo
dataList.url | 是 | String | 链接地址
dataList.time | 是 | String | 申请时间

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
    "dataList": [
      {
        "name": "产品名1",
        "productId": 1,
        "imgUrl": "http://hyj-pro.oss-cn-shenzhen.aliyuncs.com//product/logo/1551449524295.jpg",
        "url": "http://www.baidu.com",
        "time": "2019-03-19 19:04"
      }
    ],
    "dataCount": 1
  },
  "timestamp": 1552994582253
}
```
------

#### 1.5 贷款列表处的借款类型
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/page/typeList.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>贷款列表处的借款类型</td>
    </tr>
  </tbody>
</table>

##### data入参
无

##### 出参

参数名|非空|类型|说明
---|---|---|---
dataList | 是 | String | 类型数组
dataList.name | 是 | String | 类型名
dataList.typeId | 是 | int | 类型ID

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
    "dataList": [
      {
        "name": "额度高",
        "typeId": 4
      },
      {
        "name": "下款快",
        "typeId": 5
      },
      {
        "name": "期限长",
        "typeId": 6
      },
      {
        "name": "通过率高",
        "typeId": 7
      }
    ]
  },
  "timestamp": 1552994943117
}
```
------

#### 1.6 ab面切换
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/ab.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>ab面切换</td>
    </tr>
  </tbody>
</table>

##### data入参
无

##### 出参

参数名|非空|类型|说明
---|---|---|---
ab | 是 | int | 0正常页面 1 审核页面

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
    "ab": 0
  },
  "timestamp": 1552994943117
}
```
------

### 2.验证码相关

#### 2.1 短信验证码登录验证码
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/code/loginCode.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>获取短信验证码登录验证码</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
phone | 是 | String |手机号


##### 出参

参数名|非空|类型|说明
---|---|---|---
code | 是 | int| 返回代码 如果返回的不是成功需要刷新一下图形验证码的
message | 是 | String | 返回说明
data | 是 | Object | 返回数据字段
timestamp | 是 | Long | 服务器时间戳
key | 是 | String |图形验证码的key
imgCode | 是 | String |用户输的图形验证码

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {},
  "timestamp": 1514860681309
}
```

------

#### 2.2 忘记密码验证码
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/code/forgetCode.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>忘记密码验证码</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
phone | 是 | String |手机号
key | 是 | String |图形验证码的key
imgCode | 是 | String |用户输的图形验证码

##### 出参

参数名|非空|类型|说明
---|---|---|---
code | 是 | int| 返回代码  如果返回的不是成功需要刷新一下图形验证码的
message | 是 | String | 返回说明
data | 是 | Object | 返回数据字段
timestamp | 是 | Long | 服务器时间戳


sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {},
  "timestamp": 1514860681309
}
```

------

#### 2.3 图形验证码
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/code/imgCode.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>图形验证码</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
phone | 是 | String |手机号

##### 出参

参数名|非空|类型|说明
---|---|---|---
code | 是 | int| 返回代码
message | 是 | String | 返回说明
data | 是 | Object | 返回数据字段
timestamp | 是 | Long | 服务器时间戳
data.imgCode | 是 | String | 图片流(base64之后的)
data.key | 是 | String | 图片验证码的key

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
	"imgCode": "assfsdhfuosdndifbgsdfbsjkdbf",
	"key": 12435435464557567
  },
  "timestamp": 1514860681309
}
```

------

### 3.用户相关

#### 3.1  验证码登录
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/user/codeLogin.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>验证码登录</td>
    </tr>
  </tbody>
</table>

##### data入参
参数名|非空|类型|说明
---|---|---|---
phone | 是 | String| 手机号
code | 是 | String| 短信码



##### 出参
参数名|非空|类型|说明
---|---|---|---
code | 是 | int| 返回代码
message | 是 | String | 返回说明
data | 是 | Object | 返回数据字段
timestamp | 是 | Long | 服务器时间戳
token | 是 | String | 登录标识,把该标识放到请求字段中的token处



sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
	"token": "sdgkjdfhgjkshdfglhsd"
  },
  "timestamp": 1514863228068
}
```

------

#### 3.2 密码登录
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/user/passwordLogin.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>密码登录</td>
    </tr>
  </tbody>
</table>

##### data入参
参数名|非空|类型|说明
---|---|---|---
phone | 是 | String| 手机号
password | 是 | String| 密码



##### 出参

参数名|非空|类型|说明
---|---|---|---
code | 是 | int| 返回代码
message | 是 | String | 返回说明
data | 是 | Object | 返回数据字段
timestamp | 是 | Long | 服务器时间戳
token | 是 | String | 登录标识

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
	  "token": "asfkjshfskdhfkjsdhgkjdfghdfgdfg"
  },
  "timestamp": 1514863228068
}
```

------


#### 3.3 忘记密码
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/user/forgetPassword.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>忘记密码</td>
    </tr>
  </tbody>
</table>

##### data入参
参数名|非空|类型|说明
---|---|---|---
phone | 是 | String| 手机号
code | 是 | String| 短信码
password | 是 | String| 新密码



##### 出参

参数名|非空|类型|说明
---|---|---|---
code | 是 | int| 返回代码
message | 是 | String | 返回说明
data | 是 | Object | 返回数据字段
timestamp | 是 | Long | 服务器时间戳


sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {},
  "timestamp": 1514863228068
}
```

------

#### 3.4 新增点击记录
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/user/insertClickRecord.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>新增点击记录（用户进入详情页之后点击立即申请的时候调用）</td>
    </tr>
  </tbody>
</table>

##### data入参
参数名|非空|类型|说明
---|---|---|---
productId | 是 | int| 产品ID



##### 出参

参数名|非空|类型|说明
---|---|---|---
code | 是 | int| 返回代码
message | 是 | String | 返回说明
data | 是 | Object | 返回数据字段
timestamp | 是 | Long | 服务器时间戳


sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {},
  "timestamp": 1514863228068
}
```

------

