# 后台中心api接口文档

##更新记录

### 2020-04-23 更新接口线上地址

1. http://www.warmtel.com  更改为: http://it.warmtel.com

2. 登录接口地址:  http://it.warmtel.com/api/login

### 2020-02-21 更新文档
1. 增加回复列表接口、添加回复、删除、修改接口
2. 调整目录结构

## 1. 用户模块

### 1.1 登录接口

| 请求url地址 | /api/login                                                   |
| ----------- | ------------------------------------------------------------ |
| 请求方式    | post                                                         |
| 请求参数:   | string : username	string: password                        |
| 响应数据    | //登录成功响应用<br/>{<br/>  "resultCode": 1,<br/>  "resultInfo": {<br/>    "m_id": 1,<br/>    "username": "zhousir",<br/>    "password": "a665a45920422f9d417e4867efdc4fb8a04a1f3fff1fa07e998e86f7f7a27ae3",<br/>    "headerimg": "/upload/fileHeader-1577971828005.jpg",<br/>    "createtime": "2020-01-09T01:14:58.000Z",<br/>    "nick": "周sir"<br/>  },<br/>  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiemhvdXNpciIsIm9yaWdpbkV4cCI6MTU3ODUzODM4NTkxNywiaWF0IjoxNTc4NTM0Nzg1fQ.sJR4Zpja4s4HQVxUX5qb6Kd2766Ig6X_z5DR2z9mI04"<br/>}<br/>//登录失败响应<br/>	{<br/>       "resultCode": -1,<br/>       "resultInfo": "用户名密码出错!"<br/>    } |



### 1.2 退出
请求url: /api/logout
请求方式: get
请求参数： 无
响应数据

```json
{
  "resultCode": 1,
  "resultInfo": "ok"
}
```
### 1.3 用户列表
请求url：/api/list
请求方式: get
请求头: author='afdaewrqwre'
请求参数: 无
响应数据:

```json
//成功
{
  "resultCode": 1,
  "resultInfo": [
    {
      "uid": 1,
      "username": "admin",
      "password": "123"
    },
    {
      "uid": 8,
      "username": "root",
      "password": "123"
    },
    {
      "uid": 9,
      "username": "张三",
      "password": "123"
    },
    {
      "uid": 11,
      "username": "小明",
      "password": "222"
    },
    {
      "uid": 12,
      "username": "王二",
      "password": "333"
    }
  ]
}

//失败
	{
       "resultCode": -1,
       "resultInfo": "没有数据"
    }
```
### 1.4  用户列表分页

请求url：/api/list_page?pageNo=1
请求方式: get
请求参数: pageNo=1  //当前页号
响应数据:

```json
//成功
{
    resultCode: 1,
    resultInfo: {
    total: 23,
    currentNo: "1",
    pageSize:5,
    list: [
        {
            uid: 83,
            username: "tttt",
            password: "323",
            headerimg: "/upload/fileHeader-1560910892199.jpg"
        },
        {
            uid: 82,
            username: "ff",
            password: "fff",
            headerimg: null
        },
        {
            uid: 81,
            username: "ggg",
            password: "dd1",
            headerimg: null
        },
        {
            uid: 80,
            username: "dd",
            password: "ss1",
            headerimg: "/upload/fileHeader-1560910600216.jpg"
        },
        {
            uid: 79,
            username: "dd",
            password: "112",
            headerimg: null
        }
    ]
    }
}

//失败
	{
       "resultCode": -1,
       "resultInfo": "没有数据"
    }
```

### 1.5 删除用户
请求url: /api/delete
请求方式: get
请求头: author='afdaewrqwre'
请求参数: 
	uid  //用户id
响应数据

```json
//成功
{
  "resultCode": 1,
  "resultInfo": "ok"
}
//失败
{
  "resultCode": -1,
  "resultInfo": "no"
}
```
### 1.6 批量删除用户
请求url: /api/deletebatch
请求方式: post
请求头: token
请求参数: 
	 ids="1,2,3,4" //用户id,逗号分隔
响应数据
```json
//成功
{
  "resultCode": 1,
  "resultInfo": "ok"
}
//失败
{
  "resultCode": -1,
  "resultInfo": "no"
}
```
### 1.7 查询用户根据id
请求url: /api/find
请求方式: get
请求参数: 
	id   //用户id
响应数据
```json
{
    resultCode: 1,
    resultInfo: {
        uid: 127,
        username: "miss",
        password: "5994471abb01112afcc18159f6cc74",
        headerimg: "/upload/fileHeader-1578118354963.jpg"
    }
}
```
### 1.8 修改用户 根据id
请求url: /api/update
请求方式: post
请求参数:
	id			//用户id
	username  	//用户名
	psw			//密码
	
响应数据
```json
{
  "resultCode": 1,
  "resultInfo": "ok"
}
```

### 1.9 添加用户

请求url: /api/add
请求方式: post
请求参数
	username  //用户名
	psw		  //密码
	fileHeader // 头像
响应数据
```json
{
  "resultCode": 1,
  "resultInfo": "ok"
}
```



### 1.10 文件上传

请求url: /api/uploadFile
请求方式: post
请求参数： headerImg
响应数据
http://ip/abcafa.jpg


### 1.11 动态菜单
请求url: /api/sysmenu
请求方式:get
请求参数:无
响应数据
```json
{
    code: 200,
    sysmenu: [
        {
        path: "/main",
        name: "main",
        component: "Main",
        meta: {
            requireAuth: true,
            title: "用户管理"
        },
        iconCls: "el-icon-s-custom",
        hidden: true,
        children: [
            {
            path: "/user/list",
            name: "user_list",
            meta: {
            title: "用户列表"
            },
            iconCls: "el-icon-s-goods",
            hidden: true,
            component: "UserList"
            },
            {
            path: "/user/add",
            name: "user_add",
            meta: {
            title: "添加用户"
            },
            iconCls: "el-icon-user-solid",
            hidden: true,
            component: "UserAdd"
            }
        ]
        },
        {
            path: "/main",
            name: "main",
            component: "Main",
            iconCls: "el-icon-s-cooperation",
            meta: {
            requireAuth: true,
            title: "商品管理"
            },
            hidden: true,
            children: [
                {
                path: "/product/list",
                name: "product_list",
                meta: {
                title: "商品列表"
                },
                iconCls: "el-icon-s-order",
                hidden: true,
                component: "ProductList"
                },
                {
                path: "/product/add",
                name: "product_add",
                meta: {
                title: "添加栏目"
                },
                iconCls: "el-icon-s-data",
                hidden: true,
                component: "ProductAdd"
                }
            ]
        },
        {
          "path": "/main",
          "name": "main",
          "component": "Main",
          "iconCls": "el-icon-s-order",
          "meta": {
            "requireAuth": true,
            "title": "日志管理"
          },
          "hidden": true,
          "children": [
            {
              "path": "/log/list",
              "name": "log_list",
              "meta": {
                "title": "日志列表"
              },
              "iconCls": "el-icon-s-claim",
              "hidden": true,
              "component": "LogList"
            },
            {
              "path": "/log/add",
              "name": "log_add",
              "meta": {
                "title": "添加日志"
              },
              "iconCls": "el-icon-s-data",
              "hidden": true,
              "component": "LogAdd"
            }
          ]
        },
        {
          "path": "/main",
          "name": "main",
          "component": "Main",
          "iconCls": "el-icon-s-custom",
          "meta": {
            "requireAuth": true,
            "title": "操作员管理"
          },
          "hidden": true,
          "children": [
            {
              "path": "/manager/list",
              "name": "manager_list",
              "meta": {
                "title": "操作员列表"
              },
              "iconCls": "el-icon-s-claim",
              "hidden": true,
              "component": "ManagerList"
            }
          ]
        }
    ]
}
```


##2. 日志模块

###2.1 日志列表分页

请求url：/api/log/list_page
请求方式: get
请求参数:    
  pageNo 当前页号 如: pageNo=1
  name: 昵称,默认值 null 
  startTime: 开始时间,默认值 nul
  endTime: 结束时间,默认值 nul
响应数据:
```json
{
  "resultCode": 1,
  "resultInfo": {
    "total": 2,
    "currentNo": 1,
    "pageSize": 5,
    "totalNum": 1,
    "list": [
      {
        "l_id": 2,
        "content": "1. 日志学习  完成; 3. js-cooike使用 ; 总结: 熟悉模块封装，图表库使用;  计划： 完成日志功能",
        "logtime": "2020-01-09T01:34:01.000Z",
        "m_id": 1,
        "username": "zhousir",
        "nick": "周sir"
      },
      {
        "l_id": 1,
        "content": "1. 图表库echarts学习  完成; 2. 封装用户状态信和记住密码模块，3. js-cooike使用 ; 总结: 熟悉模块封装，图表库使用;  计划： 完成日志功能",
        "logtime": "2020-01-09T01:34:01.000Z",
        "m_id": 1,
        "username": "zhousir",
        "nick": "周sir"
      }
    ]
  }
}
```
### 2.2 添加日志

请求url: /api/logadd
请求方式: post
请求参数
 content 日志内容   
 logtime 日志创建时间
 mid     操作员id
响应数据
```json
{
  "resultCode": 1,
  "resultInfo": "ok"
}
```


### 2.3 删除日志

请求url: /api/log/delete
请求方式: get
请求参数
 id :  日志id
响应数据
```json
{
  "resultCode": 1,
  "resultInfo": "ok"
}
```

### 2.4 查询日志

请求url: /api/log/find
请求方式: get
请求参数
 id :  日志id
响应数据
```json
{
  "resultCode": 1,
  "resultInfo": {
    "l_id": 1,
    "content": "<p>工作日志</p><ol><li>完成日志管理模块开发</li>,
    "logtime": "2020-01-09T05:48:32.000Z"
  }
}
```


### 2.5 修改日志

请求url: /api/log/update
请求方式: post
请求参数
 id :  日志id
 content: 日志内容
响应数据
```json
{
  "resultCode": 1,
  "resultInfo": "ok"
}
```

## 3. 操作员模块
### 3.1 操作员列表
请求url: http://localhost:8088/api/manager/list
请求方式: get
请求参数: 无
响应数据
```json
  {
  "resultCode": 1,
  "resultInfo": [
    {
      "m_id": 1,
      "username": "zhousir",
      "password": "a665a45920422f9d417e4867efdc4fb8a04a1f3fff1fa07e998e86f7f7a27ae3",
      "nick": "周sir",
      "createtime": "2020-01-09T01:14:58.000Z",
      "headerimg": "/upload/fileHeader-1577971828005.jpg"
    },
    {
      "m_id": 2,
      "username": "qdx",
      "password": "a665a45920422f9d417e4867efdc4fb8a04a1f3fff1fa07e998e86f7f7a27ae3",
      "nick": "屈鼎雄",
      "createtime": "2020-01-09T01:15:42.000Z",
      "headerimg": "/upload/fileHeader-1578011746557.jpg"
    },
    {
      "m_id": 3,
      "username": "py",
      "password": "a665a45920422f9d417e4867efdc4fb8a04a1f3fff1fa07e998e86f7f7a27ae3",
      "nick": "彭宇",
      "createtime": "2020-01-09T01:16:11.000Z",
      "headerimg": "/upload/fileHeader-1578313426240.jpg"
    }
  ]
}
```



## 4. 日志回复接口

### 4.1  查看日志回复列表

请求url: /api/reply/list
请求方式: get
请求参数: logId  日志ID
响应数据
```json
  {
  "resultCode": 1,
  "resultInfo": [
    {
      "id": 1,
      "message": "收到消息，按计划进行",
      "reply_time": "2020-02-21T08:42:05.000Z",
      "nick": "周sir",
      "username": "zhousir",
      "headerimg": "/upload/fileHeader-1578301102685.jpg"
    },
    {
      "id": 2,
      "message": "好的",
      "reply_time": "2020-02-21T08:42:31.000Z",
      "nick": "彭宇",
      "username": "py",
      "headerimg": "/upload/fileHeader-1578313426240.jpg"
    },
    {
      "id": 3,
      "message": "好的",
      "reply_time": "2020-02-21T08:42:57.000Z",
      "nick": "屈鼎雄",
      "username": "qdx",
      "headerimg": "/upload/fileHeader-1578045837043.jpg"
    }
  ]
}
```


### 4.2 添加日志

请求url: /api/reply/add
请求方式: post
请求参数
 message 回复内容   
 log_id  回复日志id
 m_id 回复用户ID
响应数据
```json
{
  "resultCode": 1,
  "resultInfo": "ok"
}
```


### 4.3 删除回复

请求url: /api/reply/delete
请求方式: get
请求参数
 id :  回复id
响应数据

```json
{
  "resultCode": 1,
  "resultInfo": "ok"
}
```
### 4.4 修改回复

请求url: /api/reply/update
请求方式: post
请求参数
 id :  日志id
 message: 日志内容
响应数据
```json
{
  "resultCode": 1,
  "resultInfo": "ok"
}
```