# BootstrapBlazor.Splitting 加载动画组件

## 介绍

本Blazor组件依赖于```BootstrapBlazor```组件库开发，底层由```Splitting.js```和```gsap.js```实现。

使用该组件库之前需要先安装[BootstrapBlazor.Splitting](https://www.nuget.org/packages?q=BootstrapBlazor.Splitting)组件独立包。

可以通过```nuget```命令行安装

```bash
NuGet\Install-Package BootstrapBlazor.Splitting -Version 7.0.0
```

或者双击项目名称直接添加```ItemGroup```

```xml
<ItemGroup>
    <PackageReference Include="BootstrapBlazor.Splitting" Version="7.0.0" />
</ItemGroup>
```

## 默认示例

```html
<div>
    <Splitting/>
</div>
```

![](https://img2023.cnblogs.com/blog/2902819/202309/2902819-20230921162205327-417531846.gif)

## 自定义文本

```html
<div>
    <Splitting Text="加载中 。。。" />
</div>
```

![](https://img2023.cnblogs.com/blog/2902819/202309/2902819-20230921162217197-1480659475.gif)

## 自定义颜色

```html
<div>
    <Splitting Color="Color.Info" Text="加载中 。。。" />
</div>
```

![](https://img2023.cnblogs.com/blog/2902819/202309/2902819-20230921162224622-1648515203.gif)

## 自定义粒度

```html
<div>
    <Splitting Columns="30" Text="加载中 。。。" />
</div>
```

![](https://img2023.cnblogs.com/blog/2902819/202309/2902819-20230921162239669-1603725362.gif)
