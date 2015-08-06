# Android最简单的粒子系统

---
#巨人的肩膀
https://github.com/plattysoft/Leonids

在android世界，Leonids是一个比较简单初级的2D粒子系统，就因为其简单，所以对于认识粒子系统来说，也变得简单明了。

其类关系也比较简单，主要有ParticleSystem，Particle，ParticleField，ParticleModifier，ParticleInitializer组成。

ParticleSystem是一个具有Emittor发射器概念的管理者，管理着粒子Particle的初始化ParticleInitializer，粒子的发射后的运行状态ParticleModifier，及粒子的显示ParticleField。

![image](http://github.com/tikdik/tikdik.github.io/blob/master/%E7%B2%92%E5%AD%90%E7%B3%BB%E7%BB%9F/images/Leonids_class.PNG)

##ParticleField用户看到的粒子区域
###每个粒子是一个View
粒子要展示给用户看，那么它必须要有能够渲染的地方。我们可以给每个粒子一个View实例，然后添加到ViewTree上，这样用户就能看到了，后期更新View的translate,scale,rotate,alpha属性，也能实现粒子系统的效果。

由于粒子随时在新生和消亡，所以每个粒子是一个View的问题就会很大。
首先新建View的代价很大，每次加入视图树都会请求重新layout，耗时很长，影响性能。
其次当粒子数量很大时，视图树里面的View量也非常大，当视图需要重新Measure,Layout时，其时间花费巨大。
所以基本不会用这种玩意。

###每个粒子是一个类似Drawable的对象
从上一小节可以看出每个粒子最好是在自定义的View中，需要显示的时候去draw它。android在这块最经典的实现莫过于Drawable对象。我们可以继承Drawable对象或者仿照Drawable对象写自己的粒子系统。