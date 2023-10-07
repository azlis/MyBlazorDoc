# BootstrapBlazor组件库，Marquee 文字滚动组件

## 组件介绍

本Blazor组件依赖于```BootstrapBlazor```组件库。

使用该组件之前需要先安装[BootstrapBlazor](https://www.nuget.org/packages/BootstrapBlazor)组件库。

可以通过```nuget```命令行安装

```bash
dotnet add package BootstrapBlazor --version 7.x
```

或者双击项目名称直接添加```ItemGroup```

```xml
<ItemGroup>
    <PackageReference Include="BootstrapBlazor" Version="7.x" />
</ItemGroup>
```

## 组件用法

>Razor 代码

```csharp
<Marquee Text="@Text" 
         Color="@TextColor" 
         BackgroundColor="@BackgroundColor"
         Duration="@Duration" 
         DirecTion="@Direction" 
         FontSize="@FontSize" />

@code{
    private string BackgroundColor { get; set; } = "#000000";

    private string TextColor { get; set; } = "#ff0000";

    private string Text { get; set; } = "BootstrapBlazor 组件库，为您快速开发项目带来飞一般的感觉";

    private int FontSize { get; set; } = 72;

    private int Duration { get; set; } = 20;

    private MarqueeDirection Direction { get; set; }
}
```

## 组件效果

![img](https://img2023.cnblogs.com/blog/2902819/202310/2902819-20231007093352532-1694402709.gif)

## 组件参数

| 参数名            | 类型     | 说明        | 默认值      |
| ---------------- | -------- | ----------- | ----------- |
| `Text`           | `string?`| 滚动文本    | `null`      |
| `Color`          | `string`| 文本颜色    | `#000`      |
| `BackgroundColor`| `string`| 背景颜色    | `#fff`      |
| `Duration`       | `int`    | 持续时间(s) | `14`        |
| `Direction`      | `enum`   | 滚动方向    | `LeftToRight`|
| `FontSize`       | `int`    | 字体大小(px)| `72`        |
