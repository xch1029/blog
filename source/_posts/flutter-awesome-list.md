---
title: 使用flutter打造炫酷的list
date: 2019-06-13 13:04:40
tags: [flutter, UI]
---

使用了flutter一段时间，越来越喜欢flutter了，flutter比我们想象中的强大。这篇文章介绍了怎么使用flutter来展示一个很漂亮的list，先看下效果图。

<img src="http://qiniu.tbmao.com/awesomeList.gif">

样式还是很漂亮的，下面我们一步一步完成这个小项目。
### 开发前准备
- 我们会用到加载网络图片FadeInImage这么个widget，需要一个loading的icon，所以需要在pubspec.yaml里配置下静态资源，只有配置过的静态资源才可以在项目中使用
``` yaml
assets:
   - assets/images/
```
- 需要mock一些假数据和一些常用的常量，所以专门建了个constant.dart来管理
``` dart
    colors  # 颜色
    data  # list的数据
    # ...
```

### appBar部分
- appBar需要透明的背景这样才能将后面的图片展示出来，看起来很像沉浸式。
- 需要将elevations设置为0，这样就可以取消安卓特有的阴影效果，下面是代码:
``` dart
Scaffold(
    appBar: AppBar(
    backgroundColor: Colors.transparent,
    elevation: 0,
    title: Text(
        'flutter awesome list',
        style: TextStyle(
        color: Colors.white,
        ),
    ),
    ),
    body: HomeBody(),
);
```

### Banner部分
- 我们需要使用Transform.translate()这个weidget来将Banner部分向上移动，让appBar全部展示在banner上面，这里给的offset为offset: Offset(0, -56)，56为appBar的高度
- 下面的斜切造型需要使用ClipPath()来完成，用法有点像canvas，代码如下：
``` dart
class MyClipper extends CustomClipper<Path> {
  @override
  Path getClip(Size size) {
    Path p = Path();
    p.lineTo(size.width, 0.0);
    p.lineTo(size.width, size.height / 4.75);
    p.lineTo(0.0, size.height / 3.75);
    p.close();
    return p;
  }

  @override
  bool shouldReclip(CustomClipper oldClipper) {
    return true;
  }
}
```
- 用户信息的展示用的widget是ListTile和CircleAvatar，用法也比较简单，我直接贴代码了：
``` dart
ListTile(
    leading: CircleAvatar(
    backgroundImage: NetworkImage(CONSTANT.userAvatar),
    ),
    title: Text(
    CONSTANT.userName,
    style: CONSTANT.defaultTextStyle,
    textScaleFactor: 1.5,
    ),
    subtitle: Text(
    CONSTANT.userProfile,
    style: CONSTANT.defaultTextStyle,
    ),
)
```

### 列表展示部分
- 列表的展示使用的是ListView.builder()，两个必传参数itemCount和itemBuilder，前者控制列表的数量，后者控制item的展示，因为item的样式还是比较多的，所以抽离成单独的StatelessWidget组件：AwesomeListItem
- 我们用InkWell组件将AwesomeListItem包裹，InkWell是flutter自带的组件，这个组件的特点是点击的时候带有水墨绽开的效果。点击item的时候，我们使用Navigator.push跳转到详情页面
- 图片的展示，我们还是使用的FadeInImage，这种渐入效果的用户体验还是很不错的。然后再使用Hero()来包裹FadeInImage，这样能在页面跳转的时候提供图片之间的过渡动画，很是强大和炫酷
``` dart
Hero(
    tag: index,
    child: FadeInImage(
        image: NetworkImage(data.image),
        fit: BoxFit.cover,
        placeholder: AssetImage('assets/images/loading.gif'),
    ),
)
```

### 详情页面
最后就是详情页面的展示，这个页面并没有写什么样式，展示了从列表页跳转过来时，图片的过渡效果，有兴趣的同学可以丰富下页面的样式和内容


### 结尾
- 文章中没有张贴全部代码，感兴趣的同学可以看下源码[xch1029/awesomelist](https://github.com/xch1029/awesomelist)
- [掘金](https://juejin.im/post/5d0203ca5188256aa76bc38e)
- [简书](https://www.jianshu.com/p/a7b902b9af88)
- [颜色生成工具 来自这里](https://colorsupplyyy.com/app)
- [图片 来自这里](https://picsum.photos/)
- 受启发于 [FlutterAwesomeList](https://github.com/samarthagarwal/FlutterAwesomeList)