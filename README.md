## **一、实验目标**

1、学习使用快速启动模板创建小程序的方法；2、学习不使用模板手动创建小程序的方法。

## 二、实验步骤

列出实验的关键步骤、代码解析、截图。

#### 1、创建微信公众平台账号及安装微信小程序开发者工具

​	按照指导教程ppt及相关教程视频，我成功创建了微信公众平台账号并安装了2024最新版本的微信小程序开发者工具。打开页面如下。
![pic1](https://github.com/user-attachments/assets/b05070aa-9586-4f3c-8394-d816aa08a249)

#### 2、创建我的第一个小程序项目

​	由于本实验不涉及云服务端的使用，因此后端服务选择为**不使用云服务**。

![pic2](https://github.com/user-attachments/assets/1bb2309a-a59a-4d3f-be8a-caa880683f5d)

#### 3、小程序代码编写

​	根据视频学习我获知：

+ **js**文件用于进行逻辑实现，对于页面效果进行实现。
+ **json**文件负责标题栏及状态栏。
+ **wxml**文件管理页面中的部件组成。
+ **wxss**文件管理页面的排布美观。

​	接下来我将分文件进行我的代码解析。

------------------------

```js
/*index.wxml*/
<view class='container'>
  <image src='{{imagename}}'></image>
  <text>{{name}}</text>
  <button open-type='getUserInfo' bindgetuserinfo="getCJInfo">点击获取头像和昵称</button>
</view>
```

- {{}}用于实现动态变量，此处分别使用的{{imagename}}和{{name}}将在js文件中定义数据内容。

- button中open-type='getUserInfo' 用于获取用户的信息；bindgetuserinfo='getCJInfo'用于在点击按钮时触发后续反应调用getCJInfo函数。

  >由于2024版本微信平台取消使用getUserInfo获取用户信息的接口，因此最终实验呈现无法实现个人头像及昵称的转换。



------------------

```js
/* index.wxss */
.container{
  height:100vh;
  display:flex;
  flex-direction:column;
  align-items:center;
  justify-content:space-around;
}
image{
  width:500rpx;
  height:500rpx;
  border-radius: 50%;
}
text{
  font-size: 50rpx;
  color:darkgreen;
}
```

- container是上述wxml文件定义的类，类在定义时需要在类名前加**.**。
- 以上三个板块分别定义了页面整体排版、头像图片格式及文本格式，以保证页面美观。

-------------------------

```js
/*index.js*/  
data: {
    name:'Hello World',
    imagename:'/image/wx_image.png'
  },
  
  getCJInfo:function(e){
  console.log(e.detail.userInfo)
  let info=e.detail.userInfo;
  this.setData({
    name:info.NickName,
    imagename:info.avatarUrl
  })
}
```

- data中包含的是动态数据变量，其中所包含的内容将在在初始页面中对应name及imagename中呈现，可以实现变化。
- getCJInfo用于获取用户数据并进行修改。console.log(e.detail.userInfo)用于在控制台获取用户数据，之后利用info获取用户数据并替换页面初始数据实现页面的动态变化。

​	由于版本更新无法获取用户信息，但是为了呈现页面效果，我选择直接进行图片和昵称的替换而没有进行用户信息获取后的替换，即修改后的getCJInfo代码如下：

```js
getCJInfo:function(e){
  console.log(e.detail.userInfo)//显示仍未空用户信息
  this.setData({
    name:'快乐小狗',
    imagename:'/image/my_image.jpg'
  })//对页面信息进行直接替换
```

----------

```json
/*app.json*/
{
  "pages": [
    "pages/index/index"
  ],
    "window": {
      "navigationBarBackgroundColor": "#056608",
      "navigationBarTitleText": "小程序",
      "backgroundTextStyle": "light"
    }
}
```

- 以上分别定义了标题栏色彩、标题栏主题及背景风格。

-------------------------

## 三、程序运行结果

​	页面初始效果如下：![pic3](https://github.com/user-attachments/assets/4956c653-7c0e-423c-9c25-b5cb193b7bb5)


​	尝试获取用户信息失败情况下点击按钮后效果如下：

![pic4](https://github.com/user-attachments/assets/2ab38c25-19af-4ffe-aa90-c3d799da49ad)


​	修改代码直接进行信息修改后点击按钮后效果如下：

![pic5](https://github.com/user-attachments/assets/69dcdb1c-6dfb-4c3f-b019-0a2976fd79bb)


​	**由于无法获取用户信息，因此在console调控台的运行结果仍未空用户信息。**

## 四、问题总结与体会

描述实验过程中所遇到的问题，以及是如何解决的。有哪些收获和体会，对于课程的安排有哪些建议。

​	在实验过程中，由于微信公众平台版本更新，导致自带接口getUserInfo无法正常使用，因此无法通过系统自带工具实现头像和昵称的获取。我通过查询微信平台文档进行查询，发现其涉及的内容还未正式学习，正值高老师提出此次实验版本更新问题影响实验因此暂不需解决此问题。因此我先进行此步实验原始内容的学习，希望在接下来几周的学习中能够通过学习最新版本的微信小程序开发工具成功解决此问题。

​	在此次实验中，我对于代码的编写规范有了更深一步体会，在此次代码编写中，我因为漏缺**，**导致出现报错并细心修改，同时也对于JavaScript、CSS语言的编写进行了进一步地练习，后续我也会继续加强编程的练习。

​	最后，虽然只是一个很简单的小程序，但的确是我对小程序编写的第一次尝试，对编写过程中一步一步看到页面变得美观深深欣慰，相信经过一个夏季学期的练习，我将会更好地掌握这门技能！
