## BootstrapBlazor组件库，在你的Blazor应用程序中添加一个看板娘

效果如图
![img](https://img2023.cnblogs.com/blog/2902819/202307/2902819-20230711201306161-1786295477.png)

这里主要用到了[```BootstrapBlazor```](https://www.blazor.zone/live2ddisplay)组件库的[```Live2D 插件```](https://www.blazor.zone/live2ddisplay),本插件基于pixi-live2d-display，并且支持所有版本的 Live2D 模型。

使用时只需要在```nuget```安装```BootstrapBlazor.Live2DDisplay```组件包，在MainLaout.razor中，添加以下代码，就可以全局生效了！
```html
@inherits LayoutComponentBase

<div class="page">
    <div class="sidebar">
        <NavMenu />
    </div>

    <main>
        <div class="top-row px-4">
            <a href="https://docs.microsoft.com/aspnet/" target="_blank">About</a>
        </div>

        <article class="content px-4">
            @Body
        </article>
    </main>
    <Live2DDisplay Source="https://cdn.jsdelivr.net/gh/guansss/pixi-live2d-display/test/assets/shizuku/shizuku.model.json"
                   Scale="0.2" 
                   Position=LivePosition.BottomLeft 
                   BackgroundAlpha="false"/>
</div>
```

![img](https://img2023.cnblogs.com/blog/2902819/202307/2902819-20230711203247785-2111576714.png)
