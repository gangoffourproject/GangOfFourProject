

**你很棒（暂定）公众号**
--------------

>你很棒公众号是一个视自我激励、传递正能量为己任的微信公众号。它就是一个热心的朋友，定时地为你输送真诚的祝福；它更是一面镜子，透过它，你能见证自己的成长；它更是一个社区，在社区里，你能找到一帮志同道合的朋友。
![主界面](http://www.xiangpipi.com/test/Overview.jpg)


**功能模块介绍**
----------
**主界面**
>主界面介绍公众号的功能以及具体操作方法。对于首次关注的用户，自动回复该条图文消息。除此之外，系统每天推送一条编辑好的图文消息，包括公众号新增功能介绍、新加入朋友信息等等。

**菜单项**

> - 励志书舍
 *跳转到对应的励志书籍微店，待定*
 >- 定制祝福
 *跳转到定制页面，逐步引导用户为自己定制祝福内容、发送频率*
> - 励友帮
 *基于地理位置的展示公众号用户的分布情况，用户点击任何一个点，能够看到他/她的励志足迹*

**业务逻辑**

> - 用户的关注、取消关注
```sequence
title: 关注 
Wechat User->Our Server: Send request to entrance.php page
Note right of Our Server: Check user care or not, if not record it into db
Our Server->Wechat User: Send predefined welcome news type message as response
```
```sequence
title:取消关注
Wechat User->Our Server: Send request to entrance.php page
Note right of Our Server: Change user status in db
Our Server->Wechat User: Send questionnaire.php as response
Note right of Wechat User:User fill up a form
Wechat User->Our Server: Submit form data
Note right of Our Server: Extract feedback and save it into db 
Our Server->Wechat User: Send predefined acknowledgement news type message as response
```
> - 群发消息

*群发消息数量不大，而且内容需要精心编制，目前维护在微信公众平台管理界面比较妥当*
> - 定制祝福

*定制祝福是用户操作的主要界面，通过它可以引导用户输入关键信息，系统录入相关信息，定时推送消息给用户*

> - 励友帮

*展示一幅地图，显示其它用户的位置情况，同时，可以查看该用户的励志足迹*

**数据库表结构**

 - 用户表(user)
 
      Column Name | Type | Length | Nullable | Default Value | Key | Comment
      --- | ---
      ID | INT | - | false | - | X(1) | 用户唯一标示 
      SUBSCRIBE | BOOLEAN | - | false | true | - | 是否订阅
      SUBSCRIBETIME | DATE | - | false | - | - | 订阅时间 
      SOURCE | INT | - | false | 1 | - | 1公众平台 2移动应用 3网站应用
      OPENID | VARCHAR | 64 | false | - | X(2) | 用户在微信内部的标示
      NICKNAME | VARCHAR | 64 | true | - | - | 用户昵称
      SEX | INT | - | false | 0 | - | 0未知 1男性 2女性
      CITY | VARCHAR | 64 | true | - | - | 用户所在城市
      COUNTRY | VARCHAR | 64 | true | - | - | 用户所属国家
      LANGUAGE | VARCHAR | 32 | false | zh_CN | - | 语言
      UNIONID | VARCHAR | 64 | true | - | - | 用户在开发平台唯一标示
      AGE | INT | - | true | - | - | 年龄
      PROVINCE | VARCHAR | 64 | true | - | - | 用户所在省
      REMARKNAME | VARCHAR | 64 | true | - | - | 用户备注名
      PHONENUMBER1 | VARCHAR | 20 | true | - | - | 用户电话号码1
      PHONENUMBER2 | VARCHAR | 20 | true | - | - | 用户电话号码2
      PHONENUMBER3 | VARCHAR | 20 | true | - | - | 用户电话号码3
      EMAIL1 | VARCHAR | 64 | true | - | - | 邮箱1
      EMAIL2 | VARCHAR | 64 | true | - | - | 邮箱2
      BIRTHDAY | VARCHAR | 8 | true | - | - | 生日
      CONSTELLATION | INT | - | true | - | - | 1-12星座名
      BLOODTYPE | INT | - | true | - | - | 1A型 2B型 3 AB型 4 O型
      RENEWDATE | TIMESTAMP | - | false | - | - | 更新时间
      GROUPID | INT | - | false | - | - | 用户分组ID
      LEVELID | INT | - | false | - | - | 用户等级

 - 用户分组信息表(groupinfo)
 
    Column Name | Type | Length | Nullable | Default Value | Key | Comment
     --- | --- 
     ID | INT | - | false | - | X(1) | 分组标示
     NAME | VARCHAR | 64 | false | - | - | 组名称 
     MEMO | VARCHAR | 255 | false | - | - | 备注事项
     RENEWDATE | TIMESTAMP | - | false | - | - | 更新时间
      
 - 用户等级表(levelinfo)
 
   Column Name | Type | Length | Nullable | Default Value | Key | Comment
     --- | ---
     ID | INT | - | false | - | X(1) | 等级ID
     NAME | VARCHAR | 64 | false | - | - | 等级名称
     MEMO | VARCHAR | 255 | false | - | - | 备注事项
     RENEWDATE | TIMESTAMP | - | false | - | - | 更新时间
      
 - 用户关注信息表(uerintent)
  
     Column Name | Type | Length | Nullable | Default Value | Key | Comment
      --- | --- 
      ID | INT | - | false | - | X(1) | 关注信息ID
      USERID | INT | - | false | - | - | 用户ID
      TOPICID | INT | - | false | 1 | - | 用户关注主题ID
      SYSMESSAGEID | INT | - | true | null | - | 系统消息模板ID
      USERMESSAGEID | INT | - | true | null | - | 用户消息模板ID          
      RENEWDATE | TIMESTAMP | - | false | - | - | 更新时间
 

 - 消息主题表(topic)

 Column Name | Type | Length | Nullable | Default Value | Key | Comment
    --- | --- 
    ID | INT | - | false | - | X(1) | 消息主题ID
    NAME | VARCHAR | 64 | false | - | - | 主题名称
    FATHERID | INT | - | false | -1 | - | 父主题ID
    DESCRIPTION | VARCHAR | 255 | true | - | - | 属性描述
         
 - 系统消息表(sysmessage)
 
 Column Name | Type | Length | Nullable | Default Value | Key | Comment
    --- | --- 
ID | INT | - | false | - | X(1) | 预定义消息ID
TYPE | INT | - | false | - | - | 消息类型 1 文本 2 图片 3 图文 4 语音 5 视频 6 地理位置 7 链接 8 事件
TOPICID | INT | - | false | - | - | 消息主题属性ID
CONTENT | VARCHAR |  | false | - | - | 预定义消息内容 voice/image为文件位置，可以包含格式符号
 
 - 消息表(usermessage)
 
 Column Name | Type | Length | Nullable | Default Value | Key | Comment
    --- | --- 
ID | INT | - | false | - | X(1) | 用户预定义消息ID
USERID | INT | - | false | - | - | 用户ID
TYPE | INT | - | false | - | - | 消息类型 1 文本 2 图片 3 图文 4 语音 5 视频 6 地理位置 7 链接 8 事件
TOPICID | INT | - | false | - | - | 消息主题属性ID
CONTENT | VARCHAR |  | false | - | - | 预定义消息内容 voice/image为文件位置，可以包含格式符号
ISPUBLIC | BOOLEAN | - | false | true | - | 是否公开
 
 - 发送消息表(sentmessage)

 Column Name | Type | Length | Nullable | Default Value | Key | Comment
    --- | --- 
ID | INT | - | false | - | X(1) | 发送消息ID
USERID | INT | - | false | - | - | 用户ID
SYSMESSAGEID | INT | - | false | - | - | 预定义消息ID
USERMESSAGEID | INT | - | false | - | - | 用户自定义消息ID
CONTENT | VARCHAR | 500 | false | - | - | 发送的消息内容
RENEWDATE | TIMESTAMP | - | false | - | - | 更新时间


 - 用户成就表(待定)
 - 消息频度表(待定) 
