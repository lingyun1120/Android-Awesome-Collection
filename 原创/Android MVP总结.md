# ANDROID架构 MVP篇#

**无论是MVP还是什么架构，最终的目的都是写出易读性和测试性强的代码。所以不要对于架构钻牛角尖，过度设计不可取。在实际开发中架构自然会跟着升级。谨记！均衡合理！！**

> 
Google官方MVP项目 [https://github.com/googlesamples/android-architecture](https://github.com/googlesamples/android-architecture)  
- todo-mvp/ Basic Model-View-Presenter architecture.  
- todo-mvp-loaders/ Based on todo-mvp, fetches data using Loaders.  
- todo-databinding/ Based on todo-mvp, uses the Data Binding Library.  
- todo-mvp-clean/ Based on todo-mvp, uses concepts from Clean Architecture.  
- todo-mvp-dagger/ Based on todo-mvp, uses Dagger2 for Dependency Injection  
- todo-mvp-contentproviders/ Based on todo-mvp-loaders, fetches data using Loaders and uses Content Providers  
- todo-mvp-rxjava/ Based on todo-mvp, uses RxJava for concurrency and data layer abstraction.  

作为官方例子，有很多学习之处，多多研究，想必一定会有所收获。

## 文章推荐 ##
> 这部分内容是一些好文章的索引

1.	来自简书“diygreen”的文章：这两篇文章非常不错，总结的很完善。    
	[Android MVP 详解（上）](http://www.jianshu.com/p/9a6845b26856)  
	[Android MVP 详解（下）](http://www.jianshu.com/p/0590f530c617)  
2.	来自简书“仙鬼”的系列文章：由浅入深地学习  
	[Android MVP初探](http://www.jianshu.com/p/f8a029f6add5) 最简单MVP框架 Model-View-Presenter  
	[Android MVP进阶](http://www.jianshu.com/p/49e3d1c5d605) 对上面MVP的优化：View公共方法的提取、Present中View的判空  
	[Android MVP高级](http://www.jianshu.com/p/d5828ea38b3c) 结合Activity和Fragment的生命周期，加入Loader 对应官方例子todo-mvp-loaders  
	[Android MVP扩展](http://www.jianshu.com/p/feb1d98f8895) DataLayer, 也就是Model层; DomainLayer, 也就是UseCase层; PresentationLayer，也就是Presenter+UI层  
3.	[Android架构系列-MVP架构的实际应用](http://www.jianshu.com/p/33bdf6a0af23)  
	![](http://upload-images.jianshu.io/upload_images/1594931-cc82474f58545ff1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  
	在原有的P层中加入Interactor，将P层的逻辑更加细化。Interactor的使用根据业务具体情况，非必须。  

## 基于MVP的开源项目 ##
1. [极客日报: 一款纯粹的阅读App，基于Material Design + MVP + RxJava + Retrofit + Dagger2 + Realm + Glide](https://github.com/codeestX/GeekNews)  
	#### 包目录  
	|--app  
	&emsp;&emsp;【Application和常量】  
	|--base  
	&emsp;&emsp;【BaseView BseePresenter BaseActivity BaseFragment etc.】  
	|--component  
	&emsp;&emsp;【ACache CrashHandler ImageLoader RxBus】  
	|--di  
	&emsp;&emsp;【dagger2】  
	|--model  
	&emsp;&emsp;【bean db http 和网络、数据库相关的逻辑 Retrofit + Realm】   
	|--presenter  
	&emsp;&emsp;【链接model和ui的p层】  
	|--ui  
	&emsp;&emsp;【具体业务UI相关：采用模块化分割：如main、wechat、zhihu，各个模块由activity、adapter、fragment等组成】  
	|--util  
	&emsp;&emsp;【工具类】  
	|--widget  
	&emsp;&emsp;【自定义控件】  

	#### 采用Contact来管理View和Presenter  
		
		public interface MainContract {
    		interface View extends BaseView{
    		}
    		interface  Presenter extends BasePresenter<View> {
    		}
		}

	
2. [Mosby 框架: 一种解决Activity/Fragment生命周期在屏幕翻转等场景下对Presenter的处理的思路。](https://github.com/sockeqwe/mosby)  
	译文：[http://www.jcodecraeer.com/a/anzhuokaifa/androidkaifa/2015/0528/2945.html](http://www.jcodecraeer.com/a/anzhuokaifa/androidkaifa/2015/0528/2945.html)  
	
3.	[MVPArms 一个整合了大量主流开源项目的Android Mvp快速搭建框架](https://github.com/JessYanCoding/MVPArms)
	- [`Mvp`Google官方出品的`Mvp`架构项目，含有多个不同的架构分支(此为Dagger分支).](https://github.com/googlesamples/android-architecture/tree/todo-mvp-dagger/)
	- [`Dagger2`Google根据Square的Dagger1出品的依赖注入框架，通过apt动态生成代码，性能优于用反射技术依赖注入的框架.](https://github.com/google/dagger)
	- [`Rxjava`提供优雅的响应式Api解决异步请求.](https://github.com/ReactiveX/RxJava)
	- [`RxAndroid`为Android提供响应式Api.](https://github.com/ReactiveX/RxAndroid)
	- [`Rxlifecycle`在Android上使用rxjava都知道的一个坑，就是生命周期的解除订阅，这个框架通过绑定activity和fragment的生命周期完美解决.](https://github.com/trello/RxLifecycle)
	- [`Rxbinding`JakeWharton大神的View绑定框架，优雅的处理View的响应事件.](https://github.com/JakeWharton/RxBinding)
	- [`RxCache`是使用注解为Retrofit加入二级缓存(内存,磁盘)的缓存库](https://github.com/VictorAlbertos/RxCache)
	- [`Retrofit`Square出品的网络请求库，极大的减少了http请求的代码和步骤.](https://github.com/square/retrofit)
	- [`Okhttp`同样Square出品，不多介绍，做Android都应该知道.](https://github.com/square/okhttp)
	- [`Autolayout`鸿洋大神的Android全尺寸适配框架.](https://github.com/hongyangAndroid/AndroidAutoLayout)
	- [`Gson`Google官方的Json Convert框架.](https://github.com/google/gson)
	- [`Butterknife`JakeWharton大神出品的view注入框架.](https://github.com/JakeWharton/butterknife)
	- [`Androideventbus`一个轻量级使用注解的Eventbus.](https://github.com/hehonghui/AndroidEventBus)
	- [`Timber`JakeWharton大神出品Log框架，内部代码极少，但是思想非常不错.](https://github.com/JakeWharton/timber)
	- [`Glide`此库为本框架默认封装图片加载库，可参照着例子更改为其他的库，Api和`Picasso`差不多,缓存机制比`Picasso`复杂,速度快，适合处理大型图片流，支持gfit，`Fresco`太大了！，在5.0一下优势很大，5.0以上系统默认使用的内存管理和`Fresco`类似.](https://github.com/bumptech/glide)
	- [`Realm`速度和跨平台性使它成为如今最火的数据库,美中不足的就是so库太大](https://realm.io/docs/java/latest/#getting-started)
	- [`LeakCanary`Square出品的专门用来检测`Android`和`Java`的内存泄漏,通过通知栏提示内存泄漏信息](https://github.com/square/leakcanary)
	- [`RxErroHandler``Rxjava`错误处理库,可出现错误后重试](https://github.com/JessYanCoding/RxErrorHandler)

4.	
	