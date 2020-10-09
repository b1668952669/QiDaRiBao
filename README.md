# QiDaRiBao
安卓小项目 齐大日报 新闻api接口  
挺有意思的小东西，包括 文章，图片，视频  

----------------------------------------------------------  
摘  要  
互联网科技的发展让新闻的传播从报纸、广播、电视等方式发展到了网页以及最近几年兴起的手机app客户端，人们获取新闻的方式变得异常容易。手机上的新闻阅读app让大家随时随地掏出手机即可看天下事，手机新闻app不再是一个简简单单的新闻获取工具，单一的新闻资讯平台很难满足人们的阅读需求，服务平台预留的api接口可以解决这个问题，为用户提供个性化、更有价值的新闻。  
关键词：Android；新闻；API；  

----------------------------------------
 项目结构设计  
 底部标签栏  
最外层使用FragmentTabHost作为底部标签栏，然后第二层嵌套TabLayout + viewpager 显示内容，FragmentTabHost代表整个底部导航栏，它包含的每一个Item，称之为TabSpec，点击可以切换到相应的Fragment分页。TabSpec里面需要有指示器Indicator，用来设置样式。  
相较于RadioButton（RadioGroup）+ Fragment的实现方式，FragmentTabHost实现简单，对资源的控制相对较好。使用FragmentTabHost需要注意以下几点：  
（1）.  使用 v4 的FragmentTabHost  
（2）.  FragmentTabHost需要使用Android自带的id  
        @android:id/tabhost  
（3）.  FragmentTabHost中的FrameLayout也需要使用自带id  
        @android:id/tabcontent  
      因为实现的是底部菜单，底部的FrameLayout设置为0dp  
      真正展示内容的是上方的FrameLayout  
 
新闻列表  
新闻列表使用Toolbar + fragment显示，Toolbar 是 Android 5.0 推出的一个 Material Design 风格的导航控件 ,用来取代之前的 Actionbar 。与 Actionbar 相比，Toolbar 明显要灵活的多。它不像 Actionbar 一样，一定要固定在Activity的顶部，而是可以放到界面的任意位置。  

 变换动画  
变换动画有四种 ：alpha（透明度）、translate（平移）、rotate（旋转）、scale（伸缩），动画可以在xml实现，需要在res文件夹下新建一个anim文件夹，把xml文件放在这里；当然也可以在代码中实现。一般情况，APP中页面转场是整体统一的，但有时为了表达页面之间的从属、并列等关系，我们可能会采用不同的转场动画。在这里我们使用了rotate类型的anim动画达到使app更加顺畅的目的。  
 本章小结  
系统采用FragmentTabHost 、 TabLayout 、 viewpager 、Toolbar 、 fragment等多种结构，以及使用anim动画对程序ui进行美化处理，使其更便于阅读。   
  
项目内容  
 Vitamio  
Vitamio 是一款 Android 与 iOS 平台上的全能多媒体开发框架，全面支持硬件解码与 GPU 渲染。VItamio除了支持常规的格式之外，还支持流媒体格式，M3U8格式等主流的视频格式。其接口和Android本身自带的视频播放控件相近，所以使用起来也比较简单。  
作为一款开源项目，我们需要将其导入我们的项目中再进行适配，具体使用可以参考Vitamio使用指南，或者参考官网的使用指南。需要注意的是，尽量使用MediaPlayer+Surface，不要直接使用VideoView，因为本身视频控件就非常吃内存，容易造成内存泄露。如果需要使用VideoView的话，需要以下方法：  

 IrecyclerView  
RecyclerView是Android一个更强大的控件,其不仅可以实现和ListView同样的效果,还有优化了ListView中的各种不足，Recyclerview作为一款开源控件，在我们日常使用中中太常见了，下拉刷新以及上拉加载更多成为我们app中一种基本功能。因为RecyclerView属于新增的控件,Android将RecyclerView定义在support库里。在我们添加好依赖库后便可以使用  
PhotoView  
PhotoView是一个常用的图片预览控件，主要用于Android中大图查看，例如结合ViePager完成朋友圈九宫格图片预览功能，PhotoView主要的功能有，图片手势缩放，旋转，相比ImageView，用户体验更好。  他所有的操作都是通过使用Matrix实现，而为了实现这个功能，巧妙的使用三个Matrix来实现：  
（1） mBaseMatrix 在图片设置成功后，会初始化的一个基础Matrix，是根据图片的ScaleType，对原图片进行的scale和translation操作后得到的Matrix  
（2） mSuppMatrix 这个是图片经过手势操作，变换的scale和translation  
（3） mDrawMatrix 这个是最终设置给PhotoView的Matrix，三者的关系是：  
mDrawMatrix = mSuppMatrix * mBaseMatrix  
 Glide  
Glide和Picasso一样，是一个优秀的图片加载工具库。它可以支持多种图片数据源，在对图片加载并显示时，能较好的处理好缓存、保持较低的内存占用。目前已经被Google用于其官方应用中。  
Android在使用图片的时候是相当麻烦的，因为需要一个像素一个像素地加载这些图片到内存。一个中端手机所拍摄的一张照片有2592×1936（5百万）像素，这会占用大概19M内存。如果你再加上各种好坏不一的网络下的图片请求，同时要处理缓存、图片加载等问题，焦头烂额。如果你这时候使用了一个像Glide一样经过不断优化和严格测试的图片处理库，你会庆幸你节省了大量的时间,同时也避免了很多头疼的问题。  
 channelmanager  
Channelmanager也是一款开源项目，作为频道管理模块很适合新闻类的android项目，可以对频道进行添加、删除、排序等操作。  
 

 api  
Api为不同的应用提供方便友好的接口。不同的开发者用不同的框架，甚至不同的语言编写软件都可以通过api实现共享。因为api设计的目的就是要成为一种通用语言，让不同的软件进行信息共享，故在android项目中我们选择了使用api获取新闻数据。  
 

在本项目中使用了获取网易新闻api，部分url链接如下：  
网易: http://c.m.163.com/  
独家：https://c.m.163.com/news/sub/T1370583240249.html  
NBA：https://c.m.163.com/news/sub/T1348649145984.html  
头条：https://c.m.163.com/news/sub/T1348647909107.html  
历史：https://c.m.163.com/news/sub/T1368497029546.html  
军事：https://c.m.163.com/news/sub/T1348648141035.html  
航空：https://c.m.163.com/news/sub/T1474271789612.html  
要闻：https://c.m.163.com/news/sub/T1467284926140.html  
娱乐：https://c.m.163.com/news/sub/T1348648517839.html  
财经：https://c.m.163.com/news/sub/T1348648756099.html  
科技：https://c.m.163.com/news/sub/T1348649580692.html  
数码：https://c.m.163.com/news/sub/T1348649776727.html  
  
 本章小结  
本章大致介绍了多个GitHub上的开源代码，并使其对我们的项目进行了补充，实现了有可上下刷新的新闻列表，有新闻详情页，新闻详情页中的图片可以点击放大、图片浏览，图片浏览可以左右翻页、在线视频播放功能、有栏目管理的功能，点击新闻栏目右侧的 “+”号按钮，可以对新闻频道进行管理。  
  
---------------------  
但是做出来bug挺多  
有生之年可能会再优化一下  
