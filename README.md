#  API 文档
##### version __1.0.0__
##### 内网接口地址 http://101.200.190.163:8080

<br>
### I ChangeLog

  - 2020-04-12
    - 初始化

### II 约定


- 请求报文：
  - sign:data字段的签名
  - token:登录标识
  - data:json类型  所有的入参都放里面
  - data.timestamp:时间戳 每次请求都要传(设备本地的当前时间戳)
```json
{
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


### III 目录
- [x] 1.[登录](#1登录)
  - [x] [1.1 图形码](#11-图形码)
  - [x] [1.2 登录](#12-登录)
- [x] 2.[系统用户](#2系统用户)
  - [x] [2.1 用户列表](#21-用户列表)
  - [x] [2.2 修改用户信息](#22-修改用户信息)
  - [x] [2.3 新增用户信息](#23-新增用户信息)
  - [x] [2.4 用户对应得角色ID](#24-用户对应得角色ID)
- [x] 3.[系统角色](#3系统角色)
  - [x] [3.1 角色列表](#31-角色列表)
  - [x] [3.2 修改角色信息](#32-修改角色信息)
  - [x] [3.3 新增角色信息](#33-新增角色信息)
  - [x] [3.4 角色对应得菜单ID](#34-角色对应得菜单ID)
- [x] 4.[系统菜单](#4系统菜单)
  - [x] [4.1 菜单列表](#41-菜单列表)
  - [x] [4.2 修改菜单信息](#42-修改菜单信息)
  - [x] [4.3 新增菜单信息](#43-新增菜单信息)
- [x] 5.[首页数据面板](#5首页数据面板)
  - [x] [5.1 数据面板数据](#51-数据面板数据)
  - [x] [5.2 首页折线统计图数据](#52-首页折线统计图数据)
- [x] 6.[信息流数据面板](#6信息流数据面板)
  - [x] [6.1 首页数据](#61-首页数据)
  - [x] [6.2 首页表格数据](#62-首页表格数据)
  - [x] [6.3 数据管理页面](#63-数据管理页面)
  - [x] [6.4 表格详情数据](#64-表格详情数据)
  - [x] [6.5 渠道列表](#65-渠道列表)
  - [x] [6.6 渠道链接列表](#66-渠道链接列表)
  - [x] [6.7 新增渠道](#67-新增渠道)
  - [x] [6.8 新增渠道链接](#68-新增渠道链接)
  - [x] [6.9 新增消耗](#68-新增消耗)
  - [x] [6.10 新增开票](#68-新增开票)
- [x] 7.[安卓苹果](#8系统菜单)
  - [x] [7.1 APP列表(包名列表)](#71-APP列表(包名列表))
  - [x] [7.2 APP渠道列表(媒体列表)](#72-APP渠道列表(媒体列表))
  - [x] [7.3 新增或者修改包名](#73-新增或者修改包名)
- [x] 8.[商务](#8商务)
  - [x] [8.1 商务表格数据](#81-商务表格数据)
  - [x] [8.2 明细数据](#82-明细数据)
  - [x] [8.3 新增消耗](#83-新增消耗)
  - [x] [8.4 新增充值](#84-新增充值)
  - [x] [8.5 新增开票](#85-新增开票)
- [x] 9.[财务](#9财务)
  - [x] [9.1 首页数据](#91-首页数据)
  - [x] [9.2 财务商务数据](#92-财务商务数据)
  - [x] [9.3 财务商务明细数据](#93-财务商务明细数据)
  - [x] [9.4 财务运营数据](#93-财务运营数据)
  - [x] [9.5 财务运营明细数据](#93-财务运营明细数据)
  - [x] [9.6 发票记录列表](#93-发票记录列表)
  - [x] [9.7 修改发票](#93-修改发票)
- [x] 10.[公司](#10公司)
  - [x] [10.1 公司列表](#101-公司列表)
  - [x] [10.2 修改或者新增](#102-修改或者新增)
------

### 1.登录

#### 1.1 图形码
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/imgCode.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>获取登录时得图形码</td>
    </tr>
  </tbody>
</table>

##### data入参
无

##### data出参

参数名|非空|类型|说明
---|---|---|---
imgCode | 是 | String| base64的图片流
key | 是 | String| 该图形码的key

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
    "imgCode": "dskjfhsdfjhskdjfgksdgfdsfsdfsf",
	"key": "dskjfhsdfjhskdjfgksdgfdsfsdfsf"
  },
  "timestamp": 1552992853177
}
```
------


#### 1.2 登录
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/login.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>登录</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
imgCode | 是 | String | 用户输入的图形码
key | 是 | String | 图形码的key
loginName | 是 | String | 登陆名
password | 是 | String | 密码

##### 出参

参数名|非空|类型|说明
---|---|---|---
token | 是 | String | 登陆标识
caidans | 是 | List | 一级菜单目录
caidans.permid | 是 | String | 菜单ID
caidans.name | 是 | String | 菜单名
caidans.url | 是 | String | 菜单链接
caidans.list | 是 | String | 一级菜单下的二级目录
caidans.list.permid | 是 | String | 菜单ID
caidans.list.name | 是 | String | 菜单名
caidans.list.url | 是 | String | 菜单链接

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
	"token": "dsfsdfs",
    "caidans": [
      {
        "permid": 1,
        "name": "系统",
        "url": "url",
        "list": [
          {
            "permid": 2,
            "name": "用户管理",
            "url": "url"
          }
        ]
      }
    ]
  },
  "timestamp": 1586672660878
}
```
------


### 2.系统用户

#### 2.1 系统用户
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/user/list.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>用户列表</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
pageNum | 是 | int | 第几页
pageSize | 是 | int | 每页多少条
state | 是 | int | 状态 0 正常 1停用
loginName | 是 | String | 登陆名
stertDate | 是 | String | 创建时间开始时间
endDate | 是 | String | 创建时间结束时间

##### 出参

参数名|非空|类型|说明
---|---|---|---
list | 是 | List| 用户数组
list.id | 是 | int | 用户id
list.loginName | 是 | String | 登陆名
list.nick | 是 | String | 昵称
list.phone | 是 | String | 手机号
list.email | 是 | String | 邮箱
list.state | 是 | String | 状态 0正常 1 停用
list.creatTime | 是 | String | 创建时间
list.loginTime | 是 | String | 最后登陆时间
list.loginNum | 是 | String | 登陆次数
list.bili | 是 | String | 显示比例
count | 是 | int| 总条数(用于分页)

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
    "list": [
      {
        "id": 1,
        "loginName": "admin",
        "nick": "admin",
        "phone": "18523171796",
        "email": "641352220@qq.com",
        "state": 0,
        "creatTime": "2020-04-12 14:34",
        "loginTime": "2020-04-12 14:34",
        "loginNum": 1,
        "bili": "1"
      }
    ],
    "count": 1
  },
  "timestamp": 1586673380869
}
```

------

#### 2.2 修改用户信息
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/user/update.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>修改用户信息</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
phone | 是 | String |手机号
nick | 是 | String | 昵称
email | 是 | String | 邮箱
state | 是 | String | 0正常 1停用
bili | 是 | String | 显示比例 0.1-1
roleId | 是 | String | 角色ID

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
  "timestamp": 1514860681309
}
```

------

#### 2.3 新增用户信息
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/user/insert.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>新增用户信息</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
loginName | 是 | String | 登陆名
phone | 是 | String |手机号
nick | 是 | String | 昵称
email | 是 | String | 邮箱
state | 是 | String | 0正常 1停用
bili | 是 | String | 显示比例 0.1-1
roleId | 是 | String | 角色ID

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
  "timestamp": 1514860681309
}
```

------

#### 2.4 用户对应得角色ID
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/user/id.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>用户对应得角色ID</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
id | 是 | int | 用户ID

##### 出参

参数名|非空|类型|说明
---|---|---|---
id | 是 | int| 权限ID


sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {"id": 1},
  "timestamp": 1514860681309
}
```

------


### 3.系统角色

#### 3.1 角色列表
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/role/list.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>用户列表</td>
    </tr>
  </tbody>
</table>

##### data入参
无

##### 出参

参数名|非空|类型|说明
---|---|---|---
list | 是 | List| 角色数组
list.roleid | 是 | int | 角色id
list.rolename | 是 | String | 角色名

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
    "roles": [
      {
        "roleid": 1,
        "rolename": "admin"
      }
    ]
  },
  "timestamp": 1586673380869
}
```

------

#### 3.2 修改角色信息
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/role/update.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>修改角色信息</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
rolename | 是 | String | 角色名
cardanIds | 是 | String | 菜单的ID,多个菜单用英文","隔开,例如:"1,2,3,4"

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
  "timestamp": 1514860681309
}
```

------

#### 3.3 新增角色信息
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/role/insert.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>新增角色信息</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
rolename | 是 | String | 角色名
cardanIds | 是 | String | 菜单的ID,多个菜单用英文","隔开,例如:"1,2,3,4"

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
  "timestamp": 1514860681309
}
```

------

#### 3.4 角色对应得菜单ID
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/role/ids.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>角色对应得菜单ID</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
id | 是 | int | 角色ID

##### 出参

参数名|非空|类型|说明
---|---|---|---
ids | 是 | List| 菜单ID


sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
	 "list": [1, 2]
  },
  "timestamp": 1514860681309
}
```

------
### 4.系统菜单

#### 4.1 菜单列表
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/permission/list.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>用户列表</td>
    </tr>
  </tbody>
</table>

##### data入参
无

##### 出参

参数名|非空|类型|说明
---|---|---|---
caidans | 是 | List | 一级菜单目录
caidans.permid | 是 | String | 菜单ID
caidans.name | 是 | String | 菜单名
caidans.url | 是 | String | 菜单链接
caidans.list | 是 | String | 一级菜单下的二级目录
caidans.list.permid | 是 | String | 菜单ID
caidans.list.name | 是 | String | 菜单名
caidans.list.url | 是 | String | 菜单链接

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
    "caidans": [
      {
        "permid": 1,
        "name": "系统",
        "url": "url",
        "list": [
          {
            "permid": 2,
            "name": "用户管理",
            "url": "url"
          }
        ]
      }
    ]
  },
  "timestamp": 1586673380869
}
```

------

#### 4.2 修改菜单信息
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/permission/update.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>修改角色信息</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
permname | 是 | String | 菜单名
permurl | 是 | String | 链接
state | 是 | String | 状态 0 正常 1停用

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
  "timestamp": 1514860681309
}
```

------

#### 4.3 新增菜单信息
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/permission/insert.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>新增用户信息</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
permname | 是 | String | 菜单名
permurl | 是 | String | 链接
state | 是 | String | 状态 0 正常 1停用
parentid | 是 | int | 父级ID 0为一级菜单


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
  "timestamp": 1514860681309
}
```

------

### 5.首页数据面板

#### 5.1 数据面板数据
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/index/indexData.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>首页数据面板数据除了折线统计图</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
startTime | 是 | String | 开始时间
endTime | 是 | String | 结束时间

##### 出参

参数名|非空|类型|说明
---|---|---|---
xh | 是 | Object | 消耗
uv | 是 | Object | UV
reg | 是 | Object | 注册
login | 是 | Object | 登陆
ys | 是 | Object | 营收
android | 是 | String | 安卓
SEM | 是 | String | SEM
WC | 是 | String | 外采
iOS | 是 | String | 苹果
XXL | 是 | String | 信息流

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
    "ys": {
      "android": "0",
      "SEM": "0",
      "WC": "0",
      "iOS": "0",
      "XXL": "0"
    },
    "xh": {
      "android": "0",
      "SEM": "0",
      "WC": "0",
      "iOS": "0",
      "XXL": "0"
    },
    "uv": {
      "android": "39747",
      "SEM": "0",
      "WC": "403",
      "iOS": "5067",
      "XXL": "4"
    },
    "reg": {
      "android": "10317",
      "SEM": "0",
      "WC": "153",
      "iOS": "1693",
      "XXL": "0"
    },
    "login": {
      "android": "10317",
      "SEM": "0",
      "WC": "99",
      "iOS": "1693",
      "XXL": "0"
    }
  },
  "timestamp": 1586759179574
}
```

------

#### 5.2 首页折线统计图数据
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/index/indexImgData.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>首页数据面板数据折线统计图</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
startTime | 是 | String | 开始时间
endTime | 是 | String | 结束时间

##### 出参

参数名|非空|类型|说明
---|---|---|---
hour | 是 | String | 时间(X轴)
ys | 是 | String | 营收
uv | 是 | String | UV
xh | 是 | String | 消耗
reg | 是 | String | 注册

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
    "list": [
      {
        "hour": "00",
        "ys": 0,
        "uv": "7468",
        "xh": 0,
        "reg": "1937"
      },
      {
        "hour": "01",
        "ys": 0,
        "uv": "5072",
        "xh": 0,
        "reg": "1367"
      },
      {
        "hour": "02",
        "ys": 0,
        "uv": "3742",
        "xh": 0,
        "reg": "991"
      },
      {
        "hour": "03",
        "ys": 0,
        "uv": "2804",
        "xh": 0,
        "reg": "716"
      },
      {
        "hour": "04",
        "ys": 0,
        "uv": "2281",
        "xh": 0,
        "reg": "607"
      },
      {
        "hour": "05",
        "ys": 0,
        "uv": "2359",
        "xh": 0,
        "reg": "582"
      },
      {
        "hour": "06",
        "ys": 0,
        "uv": "4162",
        "xh": 0,
        "reg": "1056"
      },
      {
        "hour": "07",
        "ys": 0,
        "uv": "7004",
        "xh": 0,
        "reg": "1700"
      },
      {
        "hour": "08",
        "ys": 0,
        "uv": "10180",
        "xh": 0,
        "reg": "2522"
      },
      {
        "hour": "09",
        "ys": 0,
        "uv": "10282",
        "xh": 0,
        "reg": "2557"
      },
      {
        "hour": "10",
        "ys": 0,
        "uv": "10412",
        "xh": 0,
        "reg": "2388"
      },
      {
        "hour": "11",
        "ys": 0,
        "uv": "1469",
        "xh": 0,
        "reg": "357"
      }
    ]
  },
  "timestamp": 1586760612614
}
```

------

### 6.信息流数据面板

#### 6.1 首页数据
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/xxl/indexData.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>信息流数据首页</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
startTime | 是 | String | 开始时间
endTime | 是 | String | 结束时间
channel | 是 | String | 渠道,接口调用,接口后续补上,前面可以先不传

##### 出参

参数名|非空|类型|说明
---|---|---|---
time | 是 | String | 时间X轴
uv | 是 | Object | UV
reg | 是 | Object | 注册
login | 是 | Object | 登陆

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
    "list": [
      {
        "time": "2020-04-13 00",
        "reg": 0,
        "uv": 13,
        "login": 0
      },
      {
        "time": "2020-04-13 01",
        "reg": 0,
        "uv": 13,
        "login": 0
      },
      {
        "time": "2020-04-13 02",
        "reg": 0,
        "uv": 2,
        "login": 0
      },
      {
        "time": "2020-04-13 03",
        "reg": 0,
        "uv": 3,
        "login": 0
      },
      {
        "time": "2020-04-13 04",
        "reg": 0,
        "uv": 14,
        "login": 0
      },
      {
        "time": "2020-04-13 05",
        "reg": 0,
        "uv": 2,
        "login": 0
      },
      {
        "time": "2020-04-13 06",
        "reg": 0,
        "uv": 20,
        "login": 0
      },
      {
        "time": "2020-04-13 07",
        "reg": 1,
        "uv": 5,
        "login": 0
      },
      {
        "time": "2020-04-13 08",
        "reg": 0,
        "uv": 21,
        "login": 0
      },
      {
        "time": "2020-04-13 09",
        "reg": 0,
        "uv": 42,
        "login": 0
      },
      {
        "time": "2020-04-13 10",
        "reg": 0,
        "uv": 28,
        "login": 0
      },
      {
        "time": "2020-04-13 11",
        "reg": 0,
        "uv": 3,
        "login": 0
      },
      {
        "time": "2020-04-13 12",
        "reg": 0,
        "uv": 0,
        "login": 0
      },
      {
        "time": "2020-04-13 13",
        "reg": 0,
        "uv": 0,
        "login": 0
      },
      {
        "time": "2020-04-13 14",
        "reg": 0,
        "uv": 0,
        "login": 0
      },
      {
        "time": "2020-04-13 15",
        "reg": 0,
        "uv": 0,
        "login": 0
      },
      {
        "time": "2020-04-13 16",
        "reg": 0,
        "uv": 0,
        "login": 0
      },
      {
        "time": "2020-04-13 17",
        "reg": 0,
        "uv": 0,
        "login": 0
      },
      {
        "time": "2020-04-13 18",
        "reg": 0,
        "uv": 0,
        "login": 0
      },
      {
        "time": "2020-04-13 19",
        "reg": 0,
        "uv": 0,
        "login": 0
      },
      {
        "time": "2020-04-13 20",
        "reg": 0,
        "uv": 0,
        "login": 0
      },
      {
        "time": "2020-04-13 21",
        "reg": 0,
        "uv": 0,
        "login": 0
      },
      {
        "time": "2020-04-13 22",
        "reg": 0,
        "uv": 0,
        "login": 0
      },
      {
        "time": "2020-04-13 23",
        "reg": 0,
        "uv": 0,
        "login": 0
      }
    ]
  },
  "timestamp": 1586783494806
}
```

------

#### 6.2 首页折线统计图数据
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/xxl/indexTableData.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>首页数据面板数据折线统计图</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
startTime | 是 | String | 开始时间
endTime | 是 | String | 结束时间

##### 出参

参数名|非空|类型|说明
---|---|---|---
hour | 是 | String | 时间
ldyuv | 是 | String | 落地页UV
uv | 是 | String | UV
xh | 是 | String | 消耗
reg | 是 | String | 注册
login | 是 | String | 登陆

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
    "list": [
      {
        "hour": "00",
        "reg": 0,
        "login": 0,
        "uv": "13",
        "ldyuv": "77",
        "xh": 0
      },
      {
        "hour": "01",
        "reg": 0,
        "login": 0,
        "uv": "13",
        "ldyuv": "84",
        "xh": 0
      },
      {
        "hour": "02",
        "reg": 0,
        "login": 0,
        "uv": "2",
        "ldyuv": "113",
        "xh": 0
      },
      {
        "hour": "03",
        "reg": 0,
        "login": 0,
        "uv": "3",
        "ldyuv": "108",
        "xh": 0
      },
      {
        "hour": "04",
        "reg": 0,
        "login": 0,
        "uv": "14",
        "ldyuv": "114",
        "xh": 0
      },
      {
        "hour": "05",
        "reg": 0,
        "login": 0,
        "uv": "2",
        "ldyuv": "100",
        "xh": 0
      },
      {
        "hour": "06",
        "reg": 0,
        "login": 0,
        "uv": "20",
        "ldyuv": "106",
        "xh": 0
      },
      {
        "hour": "07",
        "reg": "1",
        "login": 0,
        "uv": "5",
        "ldyuv": "82",
        "xh": 0
      },
      {
        "hour": "08",
        "reg": 0,
        "login": 0,
        "uv": "21",
        "ldyuv": "82",
        "xh": 0
      },
      {
        "hour": "09",
        "reg": 0,
        "login": 0,
        "uv": "42",
        "ldyuv": "82",
        "xh": 0
      },
      {
        "hour": "10",
        "reg": 0,
        "login": 0,
        "uv": "28",
        "ldyuv": "82",
        "xh": 0
      },
      {
        "hour": "11",
        "reg": 0,
        "login": 0,
        "uv": "3",
        "ldyuv": "7",
        "xh": 0
      },
      {
        "hour": "12",
        "reg": 0,
        "login": 0,
        "uv": 0,
        "ldyuv": 0,
        "xh": 0
      },
      {
        "hour": "13",
        "reg": 0,
        "login": 0,
        "uv": 0,
        "ldyuv": 0,
        "xh": 0
      },
      {
        "hour": "14",
        "reg": 0,
        "login": 0,
        "uv": 0,
        "ldyuv": 0,
        "xh": 0
      },
      {
        "hour": "15",
        "reg": 0,
        "login": 0,
        "uv": 0,
        "ldyuv": 0,
        "xh": 0
      },
      {
        "hour": "16",
        "reg": 0,
        "login": 0,
        "uv": 0,
        "ldyuv": 0,
        "xh": 0
      },
      {
        "hour": "17",
        "reg": 0,
        "login": 0,
        "uv": 0,
        "ldyuv": 0,
        "xh": 0
      },
      {
        "hour": "18",
        "reg": 0,
        "login": 0,
        "uv": 0,
        "ldyuv": 0,
        "xh": 0
      },
      {
        "hour": "19",
        "reg": 0,
        "login": 0,
        "uv": 0,
        "ldyuv": 0,
        "xh": 0
      },
      {
        "hour": "20",
        "reg": 0,
        "login": 0,
        "uv": 0,
        "ldyuv": 0,
        "xh": 0
      },
      {
        "hour": "21",
        "reg": 0,
        "login": 0,
        "uv": 0,
        "ldyuv": 0,
        "xh": 0
      },
      {
        "hour": "22",
        "reg": 0,
        "login": 0,
        "uv": 0,
        "ldyuv": 0,
        "xh": 0
      },
      {
        "hour": "23",
        "reg": 0,
        "login": 0,
        "uv": 0,
        "ldyuv": 0,
        "xh": 0
      }
    ]
  },
  "timestamp": 1586778763404
}
```

------

#### 6.3 数据管理页面
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/xxl/TableData.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>数据管理页面</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
startTime | 是 | String | 开始时间
endTime | 是 | String | 结束时间

##### 出参

参数名|非空|类型|说明
---|---|---|---
ldyuv | 是 | String | 落地页UV
uv | 是 | String | UV
xh | 是 | String | 消耗
reg | 是 | String | 注册
login | 是 | String | 登陆

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
    "2020-04-13": {
      "reg": "1",
      "login": 0,
      "uv": "166",
      "ldyuv": "1037",
      "xh": 0
    },
	"2020-04-12": {
      "reg": "1",
      "login": 0,
      "uv": "166",
      "ldyuv": "1037",
      "xh": 0
    }
  },
  "timestamp": 1586781698734
}
```

------

#### 6.4 表格详情数据
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/xxl/TableData.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>表格详情数据</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
startTime | 是 | String | 开始时间
endTime | 是 | String | 结束时间

##### 出参

参数名|非空|类型|说明
---|---|---|---
ldyuv | 是 | String | 落地页UV
uv | 是 | String | UV
xh | 是 | String | 消耗
reg | 是 | String | 注册
login | 是 | String | 登陆

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
    "GDT81": {
      "reg": 1,
      "login": 0,
      "uv": 66,
      "ldyuv": 123,
      "xh": 0
    },
	"GDT82": {
      "reg": 1,
      "login": 0,
      "uv": 66,
      "ldyuv": 123,
      "xh": 0
    }
  },
  "timestamp": 1586783252246
}
```

------

#### 6.5 渠道列表
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/xxl/channelList.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>渠道列表</td>
    </tr>
  </tbody>
</table>

##### data入参

无

##### 出参

参数名|非空|类型|说明
---|---|---|---
channels | 是 | List | 数据列表
channel | 是 | String | 渠道标识(接口传值的)
channelName | 是 | String | 渠道名(展示给用户看的)


sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
    "channels": [
      {
        "channel": "GDT",
        "channelName": "广点通"
      },
      {
        "channel": "TT",
        "channelName": "头条"
      }
    ]
  },
  "timestamp": 1587027336860
}
```

------

#### 6.6 渠道链接列表
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/xxl/channelTwoList.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>渠道链接列表</td>
    </tr>
  </tbody>
</table>

##### data入参

无

##### 出参

参数名|非空|类型|说明
---|---|---|---
urls | 是 | List | 链接列表
urlFalg | 是 | String | 链接标识(接口传值的)
urlFalgName | 是 | String | 链接名(展示给用户看的)
url | 是 | String | 链接


sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
    "urls": [
      {
        "urlFalg": "GDT1",
        "urlFalgName": "GDT1",
        "url": "http://baidu.com/?channel=GDT1"
      },
      {
        "urlFalg": "GDT2",
        "urlFalgName": "GDT2",
        "url": "http://baidu.com/?channel=GDT2"
      }
    ]
  },
  "timestamp": 1587028932286
}
```

------

#### 6.7 新增渠道
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/xxl/insertChannel.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>新增渠道</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
channel | 是 | String | 渠道标识
channelName | 是 | String | 渠道名
urlFalg | 是 | String | 链接标识


##### 出参

无


sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {},
  "timestamp": 1587028932286
}
```

------

#### 6.8 新增渠道链接
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/xxl/insertChannelTwo.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>新增渠道链接</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
channel | 是 | String | 渠道标识
channelName | 是 | String | 渠道名
urlFalg | 是 | String | 链接标识
urlFalg | 是 | String | 渠道标识
url | 是 | String | 渠道名
urlFalgName | 是 | String | 链接标识

##### 出参

无


sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {},
  "timestamp": 1587028932286
}
```

------

#### 6.9 新增消耗
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/xxl/insertConsume.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>新增消耗</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
consumeMoney | 是 | String | 消耗金额
consumeTime | 是 | String | 消耗时间
gongsiId | 是 | String | 收款公司ID
paymentGongsiId | 是 | String | 支付公司ID 
payType | 是 | String | 1 A 2 B
remarks | 是 | String | 备注
channel | 是 | String | 渠道

##### 出参

无


sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {},
  "timestamp": 1587028932286
}
```

------

#### 6.10 新增开票
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/xxl/insertBiInvoice.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>新增开票</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
gongsiId | 是 | String | 付款公司ID
gongsiName | 是 | String | 付款公司名字
openMoney | 是 | String | 开始时间
receivableMoney | 是 | String | 应付金额
receivableSubject | 是 | String | 收款单位
receivableType | 是 | String | 结算类型 1 A 2 B
receivableGongsiId  | 是 | String | 收款公司ID
remarks | 是 | String | 备注
type | 是 | String | 1 普票 2 专票
files | 是 | String | 文件路径,多条用","隔开

##### 出参

无


sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {},
  "timestamp": 1587028932286
}
```

------

### 7.安卓苹果

#### 7.1 APP列表(包名列表)
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/xxl/appList.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>APP列表(包名列表)</td>
    </tr>
  </tbody>
</table>

##### data入参

无

##### 出参

参数名|非空|类型|说明
---|---|---|---
appId | 是 | String | 包名ID,传值用的
name | 是 | String | 包名,显示用的

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
    "list": [
      {
        "appId": 1,
        "name": "蚂蚁借款分期"
      },
      {
        "appId": 110,
        "name": "蚂蚁白卡"
      }
    ]
  },
  "timestamp": 1587100427727
}
```

------

#### 7.2 APP渠道列表(媒体列表)
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/xxl/appChannelList.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>APP列表(包名列表)</td>
    </tr>
  </tbody>
</table>

##### data入参

无

##### 出参

参数名|非空|类型|说明
---|---|---|---
appId | 是 | String | 包名ID,传值用的
name | 是 | String | 包名,显示用的
ab | 是 | String | AB面,0审核页面也就是A面 1 正常页面也就是B面
banben | 是 | String | 版本1234这种
channel | 是 | String | 渠道:VIVO,OPPO,iOS....

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
    "list": [
      {
        "appId": 1,
        "name": "蚂蚁借款分期",
		"ab": 1,
		"banben": 1,
		"channel": "VIVO"
      },
      {
        "appId": 1,
        "name": "蚂蚁借款分期",
		"ab": 1,
		"banben": 1,
		"channel": "OPPO"
      }
    ]
  },
  "timestamp": 1587100427727
}
```

------

#### 7.3  新增或者修改包名
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/xxl/insertOrUpdataApp.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>APP列表(包名列表)</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
appId | 是 | String | 包名ID
name | 是 | String | 包名
strings | 是 | String | app的附属渠道拼接字符串,拼接规则:渠道,AB面,版本-渠道,AB面,版本,例如:VIVO,1,1-OPPO,0,2

##### 出参

无
sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {},
  "timestamp": 1587100427727
}
```

------

### 8.商务

#### 8.1 商务表格数据
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/sw/tableData.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>商务表格数据</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
pageNum | 是 | String| 第几页
pageSize | 是 | String| 每页多少条
startTime | 是 | String | 开始时间
endTime | 是 | String | 结束时间
productName | 是 | String | 产品名
gongsiName | 是 | String | 公司名
settlementType | 是 | String | 结算方式 1A 2B
state | 是 | String | 状态 0 正常 1停用

##### 出参

参数名|非空|类型|说明
---|---|---|---
gongsiName | 是 | String | 公司名
productName | 是 | String | 产品名
settlementType | 是 | String | 结算方式 1A 2B
uv | 是 | String | 系统UV数
revenueUv | 是 | String | 结算UV数
unitPrice | 是 | String | 单价
revenueMoney | 是 | String | 结算金额
badMoney | 是 | String | 坏账
receivablesSubject | 是 | String | 结算主体
state | 是 | String | 状态 0 正常 1 停用
belonger | 是 | String | 归属人
productId | 是 | String | 产品ID
cz | 是 | String | 充值
ye | 是 | String | 营收
count | 是 | int | 总条数

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
    "list": [
      {
        "gongsiName": "海田科技",
        "productName": "山桃街",
        "settlementType": 0,
        "uv": 100,
        "revenueUv": 100,
        "unitPrice": 10,
        "revenueMoney": "100",
        "badMoney": "0",
        "receivablesSubject": "海田",
        "state": 0,
        "belonger": "admin",
        "productId": 1,
        "cz": "0",
        "ye": -100
      }
    ],
	"count": 1
  },
  "timestamp": 1587449222157
}
```

------

#### 8.2 明细数据

<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/sw/tableInfoData.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>明细数据</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
date | 是 | String | 月份,格式"2020-04"
productId | 是 | String | 产品ID

##### 出参

参数名|非空|类型|说明
---|---|---|---
time | 是 | String | 消耗时间
productName | 是 | String | 产品名
settlementType | 是 | String | 结算方式
uv | 是 | String | 系统UV数
revenueUv | 是 | String | 结算UV数
unitPrice | 是 | String | 单价
revenueMoney | 是 | String | 结算金额
badMoney | 是 | String | 坏账金额
receivablesSubject | 是 | String | 结算主体
receivablesType | 是 | String | 结算方式
cz | 是 | String | 充值
ye | 是 | String | 余额

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
    "list": [
      {
        "time": "2020-04-14",
        "productName": "山桃街",
        "settlementType": 1,
        "uv": 100,
        "revenueUv": 100,
        "unitPrice": 10,
        "revenueMoney": "100",
        "badMoney": "0",
        "receivablesSubject": "海田",
        "receivablesType": 1,
        "cz": "0",
        "ye": "0"
      }
    ]
  },
  "timestamp": 1587462446394
}
```

------

#### 8.3 新增消耗

<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/sw/insertData.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>新增消耗</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
badMoney | 是 | String | 坏账金额
belonger | 是 | String | 归属人
productId | 是 | String | 产品ID
receivablesSubject | 是 | String | 结算主体
receivablesType | 是 | String | 结算类型 1 A 2 B
remarks | 是 | String | 备注
revenueMoney | 是 | String | 结算金额
date | 是 | String | 时间 "2020-04-21"
revenueUv | 是 | String | 结算UV数

##### 出参

无

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {},
  "timestamp": 1587462446394
}
```

------

#### 8.4 新增充值

<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/sw/insertCZ.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>新增充值</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
productId | 是 | String | 产品ID
receivablesSubject | 是 | String | 结算主体
receivablesType | 是 | String | 结算类型 1 A 2 B
remarks | 是 | String | 备注
revenueMoney | 是 | String | 结算金额
date | 是 | String | 时间 "2020-04-21"

##### 出参

无

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {},
  "timestamp": 1587462446394
}
```

------

#### 8.5 新增开票

<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/sw/insertBiInvoice.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>新增充值</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
gongsiName | 是 | String | 公司名
openMoney | 是 | String | 开票金额
receivableMoney | 是 | String | 应收款金额
receivablesSubject | 是 | String | 收款主体
receivablesType | 是 | String | 收款类型 1A 2B
remarks | 是 | String | 备注
type | 是 | String | 1 专票 2 普票
files | 是 | String | 文件路径 多个文件路劲用","拼接

##### 出参

无

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {},
  "timestamp": 1587462446394
}
```

------

### 9.财务

#### 9.1 首页数据
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/cw/indexData.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>首页数据</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
startTime | 是 | String | 开始时间
endTime | 是 | String | 结束时间

##### 出参

参数名|非空|类型|说明
---|---|---|---
imgs | 是 | List | 顶部折线图数组
imgs.time | 是 | String | 时间
imgs.ys | 是 | String | 营收
imgs.xh | 是 | String | 消耗
az | 是 | Object | 安卓
iOS | 是 | Object | 苹果
xxl | 是 | Object | 信息流
wc | 是 | Object | 外采
sem | 是 | Object | SEM


sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
    "imgs": [
      {
        "time": "2020-04-14",
        "ys": 123,
        "xh": 1
      },
	  {
        "time": "2020-04-15",
        "ys": 123,
        "xh": 1
      }
    ],
	"az":{"ys": 123,"xh": 123},
	"iOS":{"ys": 123,"xh": 123},
	"xxl":{"ys": 123,"xh": 123},
	"wc":{"ys": 123,"xh": 123},
	"sem":{"ys": 123,"xh": 123}
  },
  "timestamp": 1587468257502
}
```

------

#### 9.2 财务商务数据
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/cw/swData.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>财务商务数据</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
startTime | 是 | String | 开始时间
endTime | 是 | String | 结束时间

##### 出参

参数名|非空|类型|说明
---|---|---|---
list | 是 | List | 顶部折线图数组
list.time | 是 | String | 时间
list.ys | 是 | String | 营收
list.hz | 是 | String | 坏账
list.cz | 是 | String | 充值
cz | 是 | String | 充值
ys | 是 | String | 营收
hz | 是 | String | 坏账
kp | 是 | String | 开票金额
nokp | 是 | String | 坏账金额

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
	"list": [
      {
        "time": "2020-04-14",
        "ys": 123,
		"hz": 123,
        "xh": 1
      },
	  {
        "time": "2020-04-15",
        "ys": 123,
		"hz": 123,
        "xh": 1
      }
    ],
    "cz": 123,
	"ys": 123,
	"hz": 123,
	"kp": 123,
	"nokp": 123
  },
  "timestamp": 1587468703876
}
```

------

#### 9.3 财务商务明细数据
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/cw/swInfoData.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>财务商务明细数据</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
startTime | 是 | String | 开始时间
endTime | 是 | String | 结束时间


##### 出参

参数名|非空|类型|说明
---|---|---|---
list | 是 | List | 数据数组
list.gongsiName | 是 | String | 公司名
list.payType | 是 | String | 1A 2B
list.collectionAccount | 是 | String | 收款账号
list.cz | 是 | String | 充值
list.xh | 是 | String | 消耗
list.hz | 是 | String | 坏账

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
	"list": [
      {
        "gongsiName": "海田",
        "payType": 1,
		"collectionAccount": "人民银行",
        "cz": 123,
		"xh": 123,
		"hz": 123
      },
	  {
        "gongsiName": "海田",
        "payType": 1,
		"collectionAccount": "人民银行",
        "cz": 123,
		"xh": 123,
		"hz": 123
      }
    ]
  },
  "timestamp": 1587468703876
}
```

------

#### 9.4 财务运营数据
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/cw/cwyyData.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>财务运营数据</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
startTime | 是 | String | 开始时间
endTime | 是 | String | 结束时间

##### 出参

参数名|非空|类型|说明
---|---|---|---
list | 是 | List | 顶部折线图数组
list.time | 是 | String | 时间
list.ys | 是 | String | 营收
list.xh | 是 | String | 消耗
az | 是 | Object | 安卓
iOS | 是 | Object | 苹果
xxl | 是 | Object | 信息流
wc | 是 | Object | 外采
sem | 是 | Object | SEM
dk | 是 | String | 打款
zs | 是 | String | 赠送
xh | 是 | String | 消耗
kp | 是 | String | 开票金额
nokp | 是 | String | 坏账金额

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
	"list": [
      {
        "time": "2020-04-14",
        "ys": 123,
        "xh": 1
      },
	  {
        "time": "2020-04-15",
        "ys": 123,
        "xh": 1
      }
    ],
    "az":{"dk": 123,"zs": 123,"xh": 123,"kp": 123,"nokp": 123},
	"iOS":{"dk": 123,"zs": 123,"xh": 123,"kp": 123,"nokp": 123},
	"xxl":{"dk": 123,"zs": 123,"xh": 123,"kp": 123,"nokp": 123},
	"wc":{"dk": 123,"zs": 123,"xh": 123,"kp": 123,"nokp": 123},
	"sem":{"dk": 123,"zs": 123,"xh": 123,"kp": 123,"nokp": 123}
  },
  "timestamp": 1587468703876
}
```

------

#### 9.5 财务运营明细数据
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/cw/yyInfoData.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>财务运营明细数据</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
startTime | 是 | String | 开始时间
endTime | 是 | String | 结束时间


##### 出参

参数名|非空|类型|说明
---|---|---|---
list | 是 | List | 数据数组
list.gongsiName | 是 | String | 公司名
list.payType | 是 | String | 1A 2B
list.collectionAccount | 是 | String | 收款账号
list.cz | 是 | String | 充值
list.xh | 是 | String | 消耗
list.zs | 是 | String | 赠送

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
	"list": [
      {
        "gongsiName": "海田",
        "payType": 1,
		"collectionAccount": "人民银行",
        "cz": 123,
		"xh": 123,
		"zs": 123
      },
	  {
        "gongsiName": "海田",
        "payType": 1,
		"collectionAccount": "人民银行",
        "cz": 123,
		"xh": 123,
		"zs": 123
      }
    ]
  },
  "timestamp": 1587468703876
}
```

------

#### 9.6 发票记录列表
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/cw/InvoiceList.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>发票记录列表</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
startTime | 是 | String | 开始时间
endTime | 是 | String | 结束时间
type | 是 | int | 1 商务 2 安卓 3 苹果 4 信息流 5 公众号 6 SEM 7 外采


##### 出参

参数名|非空|类型|说明
---|---|---|---
id | 是 | String | 发票ID	
gongsiName | 是 | String | 开票公司
type | 是 | String | 1 普票 2 专票
openMoney | 是 | String | 开票金额
receivableMoney | 是 | String | 应收金额
receivableType | 是 | String | 收款类型 1A 2B
receivableGongsiId | 是 | String | 收款公司ID
receivableSubject | 是 | String | 收款单位
state | 是 | String | 0 待审核 1 通过 2拒绝
expressId | 是 | String | 快递单号
remarks | 是 | String | 备注
creatUser | 是 | String | 创建人
creatTime | 是 | String | 创建时间
examineUser | 是 | String | 审核人
examineTime | 是 | String | 审核时间

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
	"list": [
      {
        "id": 1,
        "gongsiName": "海田",
		"type": 1,
        "openMoney": 123,
		"receivableMoney": 123,
		"receivableType": 1,
		"receivableSubject": "海田",
		"receivableGongsiId": 1,
		"state": 1,
		"expressId": 123,
		"remarks": "加急",
		"creatUser": 1,
		"creatTime": "2020-04-24",
		"examineUser": 123,
		"examineTime": "2020-04-24"
      }
    ]
  },
  "timestamp": 1587468703876
}
```

------

#### 9.7 修改发票
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/cw/updateSWInvoice.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>发票记录列表</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
state | 是 | String | 1 通过 2 拒绝
expressId | 是 | String | 快递ID
remarks | 是 | String | 备注
files | 是 | String | 文件路径,多条用","隔开



##### 出参

无

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {},
  "timestamp": 1587468703876
}
```

------

### 10.公司

#### 10.1 公司列表
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/gongsi/list.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>公司列表</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
pageNum | 是 | String| 第几页
pageSize | 是 | String| 每页多少条

##### data出参

参数名|非空|类型|说明
---|---|---|---
id | 是 | String| 公司ID
type | 是 | String| 1 甲方 2 苹果 3 安卓 4 信息流 5 SEM 6 外采 7 公众号
gongsiName | 是 | String| 公司名
payType | 是 | String| 1 A 2 B
collectionAccount | 是 | String| 收款账号
state | 是 | String| 0 正常 1 停用
count | 是 | String| 总数

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {
    "list": [
      {
        "id": 1,
        "gongsiName": "海田",
		"type": 1,
        "payType": 1,
		"collectionAccount": "人民银行",
		"state": 1
      }
    ],
	"count": 123
  },
  "timestamp": 1552992853177
}
```
------


#### 10.2 修改或者新增
<table>
  <tbody>
    <tr>
      <td>URI</td>
      <td>/gongsi/update.html</td>
    </tr>
    <tr>
      <td>描述</td>
      <td>修改或者新增</td>
    </tr>
  </tbody>
</table>

##### data入参

参数名|非空|类型|说明
---|---|---|---
id | 是 | String | 公司ID
collectionAccount | 是 | String | 收款账号
gongsiName | 是 | String | 公司名
payType | 是 | String | 1 A 2 B
state | 是 | String | 0 正常 1 停用
type | 是 | String | 1 甲方 2 苹果 3 安卓 4 信息流 5 SEM 6 外采 7 公众号

##### 出参

无

sample:
```json
{
  "code": 0,
  "message": "成功",
  "data": {},
  "timestamp": 1586672660878
}
```
------
