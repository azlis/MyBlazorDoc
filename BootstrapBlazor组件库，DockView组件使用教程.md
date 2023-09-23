# BootstrapBlazor组件库，DockView组件使用教程

使用该组件库之前需要先安装[BootstrapBlazor.Dock](https://www.nuget.org/packages/BootstrapBlazor.Dock)组件独立包。

可以通过```nuget```命令行安装

```bash
NuGet\Install-Package BootstrapBlazor.Dock -Version 7.0.11
```

或者双击项目名称直接添加```ItemGroup```

```xml
<ItemGroup>
    <PackageReference Include="BootstrapBlazor.Dock" Version="7.0.11" />
</ItemGroup>
```

重点关注DockContent的Type 属性
|属性|说明|
|-|-|
|DockContentType.Row|行排列 水平排列|
|DockContentType.Column|列排列 垂直排列|
|DockContentType.Stack|标签排列|
|DockContentType.Component|组件|

使用时添加razor如下代码

```html
<DockView Name="DockViewColumn" >
    <DockContent Type="DockContentType.Column">
        <DockComponent Title="left dock" ShowClose="false">
            <div>
                left dock
            </div>
        </DockComponent>
        <DockComponent Title="right dock" ShowClose="false">
            <div>
                right dock
            </div>
        </DockComponent>
    </DockContent>
</DockView>
```

上面的代码包含了一个外部的```DockView```容器，内部的```DockContent```支持嵌套，运行结果如图。

![img](https://img2023.cnblogs.com/blog/2902819/202308/2902819-20230804153728243-323404836.png)
