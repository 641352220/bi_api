#  API 文档
##### version __1.0.0__
##### 内网接口地址 

<br>
### I 约定


- 请求报文：
  - uid: 每个设备的唯一标识,不变且唯一
  - appId: 每个应用的ID
  - os:平台 Android / iOS
  - channel: 渠道(由后台给)
  - token:用户的登录标识
  - version:版本 内部版本 初始化为1 整形 每打次包加一
  - data:json类型  所有的入参都放里面
  - data.timestamp:时间戳 每次请求都要传
```json
{
  "uid": "a29cf5f84ad64ab1a5dbc5a58ca53628",
  "appid": 1,
  "os": "Android",
  "channel": 1,
  "token": "8edb3d300e754bad9d0e97da6d6c781e",
  "version": 1,
  "sign": "8edb3d300e754bad9d0e97da6d6c781e",
  "data": "{'timestamp':'524357435743574'}"
}
```


- 返回报文：
  - code: 返回的状态码 全局的状态码(0 成功 1失败 33token过期 44 时间戳过期 55 验签失败)
  - message:提示信息
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

### II 目录
- [x] 1.[页面接口](#1页面接口)
  - [x] [1.1 首页数据](#11-会员特权列表)
  - [x] [1.2 别的地方广告数据](#12-别的地方广告数据)
  - [x] [1.3 产品列表数据](#13-产品列表数据)
  - [x] [1.4 获取产品链接并增加UV](#14-获取产品链接并增加UV)
  - [x] [1.5 点击记录列表数据](#15-点击记录列表数据)
  - [x] [1.6 新增反馈](#16-新增反馈)
  - [x] [1.7 获取APP信息](#17-获取APP信息)
- [x] 2.[其他](#2其他)
  - [x] [2.1 图形码](#21-图形码)
  - [x] [2.2 登录短信验证码](#22-登录短信验证码)
  - [x] [2.3 验证码登录](#23-验证码登录)
  - [x] [2.4 密码登录](#24-密码登录)
  - [x] [2.5 修改登录密码](#25-修改登录密码)



------

### 1.页面接口

#### 1.1 首页数据
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/page/indexPage.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>首页的所有数据</td>
    </tr>
  </tbody>
</table>

##### data入参
参数名|非空|类型|说明
---|---|---|---
pageNum | 是 | int| 第几页,初始值为1
pageSize | 是 | int| 每页多少条

##### data出参

参数名|非空|类型|说明
---|---|---|---
bannerList | 是 | 数组| banner数据
bannerList.imgUrl | 是 | String| 图片地址
bannerList.title | 是 | String| 标题(可忽略,扩展字段)
bannerList.productId | 是 | int| 产品ID(内链产品时,通过该ID去调产品详情获取URL跳转网页)
bannerList.type | 是 | int| 类型(1内链产品 2外链(打开下面的bannerList.url链接) 3内链产品列表(拓展类型))可以根据自身情况,在终端写死,除非类型为1否则其他类型不可点击
bannerList.url | 是 | String| 图片地址
informationsList | 是 | 数组| 轮播信息
informationsList.content | 是 | String| 轮播内容
informationsList.productId | 是 | int| 产品ID
typeList | 是 | 数组| 小广告数据
bannerList.imgUrl | 是 | String| 图片地址
bannerList.name | 是 | String| 标题(可忽略,扩展字段)
bannerList.productId | 是 | int| 产品ID(内链产品时,通过该ID去调产品详情获取URL跳转网页)
bannerList.type | 是 | int| 类型(1内链产品 2外链(打开下面的bannerList.url链接) 3内链产品列表(拓展类型))可以根据自身情况,在终端写死,除非类型为1否则其他类型不可点击
bannerList.url | 是 | String| 图片地址
jrtjList | 是 | 数组| 推荐产品数据
jrtjList.imgUrl | 是 | String| 图片地址
jrtjList.name | 是 | String| 产品名
jrtjList.productId | 是 | int| 产品ID
jrtjList.rateType | 是 | int| 计息类型1 按日 2 按月
jrtjList.adver | 是 | String| 广告语
jrtjList.moneyMax | 是 | String| 可贷最大金额
jrtjList.moneyMin | 是 | String| 可贷最小金额
jrtjList.rateMin | 是 | String| 最低利率
jrtjList.loanNum | 是 | String| 下款人数
jrtjList.dayMax | 是 | String| 可贷最长期限(单位天)
jrtjList.loanTime | 是 | String| 下款时间(单位分钟)
jrtjList.label | 是 | String| 标签
jrtjList.labels | 是 | 数组| 标签数组
productList | 是 | 数组| 推荐产品数据
productList.imgUrl | 是 | String| 图片地址
productList.name | 是 | String| 产品名
productList.productId | 是 | int| 产品ID
productList.rateType | 是 | int| 计息类型1 按日 2 按月
productList.adver | 是 | String| 广告语
productList.moneyMax | 是 | String| 可贷最大金额
productList.moneyMin | 是 | String| 可贷最小金额
productList.rateMin | 是 | String| 最低利率
productList.loanNum | 是 | String| 下款人数
productList.dayMax | 是 | String| 可贷最长期限(单位天)
productList.loanTime | 是 | String| 下款时间(单位分钟)
productList.label | 是 | String| 标签
productList.labels | 是 | 数组| 标签数组

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
    "bannerList": [
      {
        "imgUrl": "https://wyd-pro.oss-cn-shenzhen.aliyuncs.com//banner/img/1507518998070.png",
        "title": "秒下款",
		"productId": 1,
		"type": 1,
        "url": "http://www.baidu.com"
      },
	  {
        "imgUrl": "https://wyd-pro.oss-cn-shenzhen.aliyuncs.com//banner/img/1507518998070.png",
        "title": "下款快",
		"productId": 1,
		"type": 1,
        "url": "http://www.baidu.com"
      }
    ],
    "informationsList": [
      {
        "content": "恭喜上海的王先生在如意贷下款3000元",
		"productId": 1
      },
	  {
        "content": "恭喜上海的王先生在如意贷下款3000元",
		"productId": 2
      }
    ],
	"typeList": [
      {
        "imgUrl": "https://wyd-pro.oss-cn-shenzhen.aliyuncs.com//banner/img/1507518998070.png",
        "name": "秒下款",
		"productId": 1,
		"type": 1,
        "url": "http://www.baidu.com"
      },
	  {
        "imgUrl": "https://wyd-pro.oss-cn-shenzhen.aliyuncs.com//banner/img/1507518998070.png",
        "name": "下款快",
		"productId": 1,
		"type": 1,
        "url": "http://www.baidu.com"
      }
    ],
	"jrtjList": [
      {
        "imgUrl": "https://wyd-pro.oss-cn-shenzhen.aliyuncs.com//banner/img/1507518998070.png",
        "name": "秒下款",
		"productId": 1,
		"rateType": 1,
		"adver": "秒下款",
		"moneyMax": "10000",
		"moneyMin": "1000",
		"rateMin": "0.3",
		"loanNum": "123432",
		"dayMax": "360",
		"loanTime": "5",
		"label": "下款快",
		"labels": ["额度高哦","下款快"]
      },
	  {
        "imgUrl": "https://wyd-pro.oss-cn-shenzhen.aliyuncs.com//banner/img/1507518998070.png",
        "name": "秒下款",
		"productId": 2,
		"rateType": 1,
		"adver": "秒下款",
		"moneyMax": "10000",
		"moneyMin": "1000",
		"rateMin": "0.3",
		"loanNum": "123432",
		"dayMax": "360",
		"loanTime": "5",
		"label": "下款快",
		"labels": ["额度高哦","下款快"]
      }
    ],
	"productList": [
      {
        "imgUrl": "https://wyd-pro.oss-cn-shenzhen.aliyuncs.com//banner/img/1507518998070.png",
        "name": "秒下款",
		"productId": 1,
		"rateType": 1,
		"adver": "秒下款",
		"moneyMax": "10000",
		"moneyMin": "1000",
		"rateMin": "0.3",
		"loanNum": "123432",
		"dayMax": "360",
		"loanTime": "5",
		"label": "下款快",
		"labels": ["额度高哦","下款快"]
      },
	  {
        "imgUrl": "https://wyd-pro.oss-cn-shenzhen.aliyuncs.com//banner/img/1507518998070.png",
        "name": "秒下款",
		"productId": 2,
		"rateType": 1,
		"adver": "秒下款",
		"moneyMax": "10000",
		"moneyMin": "1000",
		"rateMin": "0.3",
		"loanNum": "123432",
		"dayMax": "360",
		"loanTime": "5",
		"label": "下款快",
		"labels": ["额度高哦","下款快"]
      }
    ]
  },
  "timestamp": 1514535058890
}
```
------


#### 1.2 别的地方广告数据
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/page/typeListPage.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>别的地方广告数据</td>
    </tr>
  </tbody>
</table>

##### data入参
参数名|非空|类型|说明
---|---|---|---
typePosition | 是 | int| 位置标识1首页 2列表 3个人中心

##### data出参

参数名|非空|类型|说明
---|---|---|---
id | 是 | String| 会员套餐ID
content | 是 | String| 说明
adver | 是 | String| 广告语
originalPrice | 是 | String| 原价
concessionalRate | 是 | String| 优惠价


sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
	"typeList": [
      {
        "imgUrl": "https://wyd-pro.oss-cn-shenzhen.aliyuncs.com//banner/img/1507518998070.png",
        "name": "秒下款",
		"productId": 1,
		"type": 1,
        "url": "http://www.baidu.com"
      },
	  {
        "imgUrl": "https://wyd-pro.oss-cn-shenzhen.aliyuncs.com//banner/img/1507518998070.png",
        "name": "下款快",
		"productId": 1,
		"type": 1,
        "url": "http://www.baidu.com"
      }
    ]
  },
  "timestamp": 1514535058890
}
```
------

#### 1.3 产品列表数据
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/page/productListPage.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>产品列表数据</td>
    </tr>
  </tbody>
</table>

##### data入参
参数名|非空|类型|说明
---|---|---|---
pageNum | 是 | int| 第几页,初始值为1
pageSize | 是 | int| 每页多少条

##### data出参

参数名|非空|类型|说明
---|---|---|---
productList | 是 | 数组| 推荐产品数据
productList.imgUrl | 是 | String| 图片地址
productList.name | 是 | String| 产品名
productList.productId | 是 | int| 产品ID
productList.rateType | 是 | int| 计息类型1 按日 2 按月
productList.adver | 是 | String| 广告语
productList.moneyMax | 是 | String| 可贷最大金额
productList.moneyMin | 是 | String| 可贷最小金额
productList.rateMin | 是 | String| 最低利率
productList.loanNum | 是 | String| 下款人数
productList.dayMax | 是 | String| 可贷最长期限(单位天)
productList.loanTime | 是 | String| 下款时间(单位分钟)
productList.label | 是 | String| 标签
productList.labels | 是 | 数组| 标签数组


sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
	"productList": [
      {
        "imgUrl": "https://wyd-pro.oss-cn-shenzhen.aliyuncs.com//banner/img/1507518998070.png",
        "name": "秒下款",
		"productId": 1,
		"rateType": 1,
		"adver": "秒下款",
		"moneyMax": "10000",
		"moneyMin": "1000",
		"rateMin": "0.3",
		"loanNum": "123432",
		"dayMax": "360",
		"loanTime": "5",
		"label": "下款快",
		"labels": ["额度高哦","下款快"]
      },
	  {
        "imgUrl": "https://wyd-pro.oss-cn-shenzhen.aliyuncs.com//banner/img/1507518998070.png",
        "name": "秒下款",
		"productId": 2,
		"rateType": 1,
		"adver": "秒下款",
		"moneyMax": "10000",
		"moneyMin": "1000",
		"rateMin": "0.3",
		"loanNum": "123432",
		"dayMax": "360",
		"loanTime": "5",
		"label": "下款快",
		"labels": ["额度高哦","下款快"]
      }
    ]
  },
  "timestamp": 1514535058890
}
```
------

#### 1.4 获取产品链接并增加UV
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/page/GetProductUrl.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>获取产品链接并增加UV</td>
    </tr>
  </tbody>
</table>

##### data
参数名|非空|类型|说明
---|---|---|---
productId | 是 | int| 产品ID

##### data出参

参数名|非空|类型|说明
---|---|---|---
url | 是 | String| 产品链接


sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
	"url": "http://www.baidu.com"
  },
  "timestamp": 1514535058890
}
```
------

#### 1.5 点击记录列表数据
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/user/UvListPage.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>点击记录列表数据</td>
    </tr>
  </tbody>
</table>

##### data入参
无

##### data出参

参数名|非空|类型|说明
---|---|---|---
productList | 是 | 数组| 推荐产品数据
productList.imgUrl | 是 | String| 图片地址
productList.name | 是 | String| 产品名
productList.productId | 是 | int| 产品ID
productList.rateType | 是 | int| 计息类型1 按日 2 按月
productList.adver | 是 | String| 广告语
productList.moneyMax | 是 | String| 可贷最大金额
productList.moneyMin | 是 | String| 可贷最小金额
productList.rateMin | 是 | String| 最低利率
productList.loanNum | 是 | String| 下款人数
productList.dayMax | 是 | String| 可贷最长期限(单位天)
productList.loanTime | 是 | String| 下款时间(单位分钟)
productList.label | 是 | String| 标签
productList.labels | 是 | 数组| 标签数组


sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
	"productList": [
      {
        "imgUrl": "https://wyd-pro.oss-cn-shenzhen.aliyuncs.com//banner/img/1507518998070.png",
        "name": "秒下款",
		"productId": 1,
		"rateType": 1,
		"adver": "秒下款",
		"moneyMax": "10000",
		"moneyMin": "1000",
		"rateMin": "0.3",
		"loanNum": "123432",
		"dayMax": "360",
		"loanTime": "5",
		"label": "下款快",
		"labels": ["额度高哦","下款快"]
      },
	  {
        "imgUrl": "https://wyd-pro.oss-cn-shenzhen.aliyuncs.com//banner/img/1507518998070.png",
        "name": "秒下款",
		"productId": 2,
		"rateType": 1,
		"adver": "秒下款",
		"moneyMax": "10000",
		"moneyMin": "1000",
		"rateMin": "0.3",
		"loanNum": "123432",
		"dayMax": "360",
		"loanTime": "5",
		"label": "下款快",
		"labels": ["额度高哦","下款快"]
      }
    ]
  },
  "timestamp": 1514535058890
}
```
------

#### 1.6 新增反馈
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/insertFk.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>新增反馈</td>
    </tr>
  </tbody>
</table>

##### data入参
参数名|非空|类型|说明
---|---|---|---
content | 是 | String | 用户反馈内容


##### 出参
无


sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {},
  "timestamp": 1514535058890
}
```
------

#### 1.7 获取APP信息
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/getAppInfo.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>获取APP信息,主要就是AB面</td>
    </tr>
  </tbody>
</table>

##### data入参
无

##### data出参

参数名|非空|类型|说明
---|---|---|---
ab | 是 | int| 0正常页面 1审核页面
KfUrl | 是 | String| 客服地址
newapp | 是 | int| 0没有更新 1有新版本
gxType | 是 | int| 0 非强制更新 1强制更新 (也就是有没有关闭按钮的事)
content | 是 | String| 更新说明
url | 是 | String| 更新地址

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
	"ab": 0,
	"KfUrl": "http://www.baidu.com",
	"newapp": 1,
	"gxType": 0,
	"content": "更新说明",
	"url": "http://www.baidu.com"
  },
  "timestamp": 1514535058890
}
```
------

### 2.其他

#### 2.1 图形码
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/code/imgCode.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>图形码</td>
    </tr>
  </tbody>
</table>

##### 入参
无


##### data出参新增参数

参数名|非空|类型|说明
---|---|---|---
key | 是 | String | 该图形码的key
imgCode | 是 | String | 二进制的图片流

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
	"key": "sfgdskfsdghdshjfdsgj",
	"imgCode": "sfgdskfsdghdshjfdsgj"
  },
  "timestamp": 1514535058890
}
```
------

#### 2.2 登录短信验证码
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/code/loginCode.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>登录短信验证码</td>
    </tr>
  </tbody>
</table>

##### 入参
参数名|非空|类型|说明
---|---|---|---
phone | 是 | String | 手机号
key | 是 | String | 图形码的key(后端反回的)
imgCode | 是 | String | 用户输的码


##### data出参

可以不用调用图形码的接口直接调用该接口,不调用的话key和imgCode不传就行,但是如果后端返回状态码为1的时候就必须调用,因为后端逻辑为一个手机号10分钟内可以免图形码调用两次。

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {},
  "timestamp": 1514535058890
}
```

------

#### 2.3 验证码登录
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
phone | 是 | String | 手机号
code | 是 | String | 短信码
jingdu | 是 | String | 用户注册的时候的经度(非必传)
loginType | 是 | String | 登录类型 0 正常登录 1 一键登录 (根据情况固定0就行)
weidu | 是 | String | 用户注册的时候的纬度(非必传)


##### data出参

参数名|非空|类型|说明
---|---|---|---
token | 是 | String | 登录标识,后续的所有接口必须带上这个token

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
	"token": "dfeguhrguiwebciuwebf"
  },
  "timestamp": 1514535058890
}
```

------

#### 2.4 密码登录
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/user/passLogin.html</td>
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
phone | 是 | String | 手机号
password | 是 | String | 密码


##### data出参

参数名|非空|类型|说明
---|---|---|---
token | 是 | String | 登录标识,后续的所有接口必须带上这个token

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
	"token": "dfeguhrguiwebciuwebf"
  },
  "timestamp": 1514535058890
}
```

------

#### 2.5 修改登录密码
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/user/updatePassword.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>修改登录密码</td>
    </tr>
  </tbody>
</table>

##### data入参
参数名|非空|类型|说明
---|---|---|---
password | 是 | String | 密码


##### data出参
无

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
	"token": "dfeguhrguiwebciuwebf"
  },
  "timestamp": 1514535058890
}
```

------
