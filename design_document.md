

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

 - 用户表(User)
 
      Column Name | Type | Length | Nullable | Default Value | Key | Comment
      --- | ---
      ID | INT | - | false | - | X(1) | user identification 
      SUBSCRIBE |
      SUBSCRIBETIME |
      SOURCE | 
      OPENID |
      NICKNAME |
      SEX |
      CITY |
      COUNTRY |
      LANGUAGE |
      UNIONID |
      AGE |
      PROVINCE |
      REMARKNAME |
      PHONENUMBER1 |
      PHONENUMBER2 |
      PHONENUMBER3 |
      EMAIL1 |
      EMAIL2 |
      BIRTHDAY |
      CONSTELLATION |
      BLOODTYPE |
      RENEWDATE |
      GROUPID |
      LEVELID |

 - 用户分组信息表(GroupInfo)
 
    Column Name | Type | Length | Nullable | Default Value | Key | Comment
     --- | --- 
     ID |
     NAME |
     MEMO |
     RENEWDATE |
      
 - 用户等级表(LevelInfo)
 
   Column Name | Type | Length | Nullable | Default Value | Key | Comment
     --- | ---
     ID |
     NAME |
     MEMO |
     RENEWDATE | 
      
 - 用户关注信息表(UserIntent)
  
     Column Name | Type | Length | Nullable | Default Value | Key | Comment
      --- | --- 
      ID |
      USERID |
      TOPICID |           
      RENEWDATE |

 - 信息分类表(UserIntent)

 Column Name | Type | Length | Nullable | Default Value | Key | Comment
    --- | --- 
    ID |
    NAME | 
    CATEGORY | 
    SUBCATEGORY | 
    DESCRIPTION | 
         
 - 内容表
 Column Name | Type | Length | Nullable | Default Value | Key | Comment
    --- | --- 
ID |
 
 - 成就表
 - 用户消息表

