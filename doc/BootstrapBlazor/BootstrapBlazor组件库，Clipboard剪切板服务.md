# BootstrapBlazor组件库，Clipboard 剪切板服务

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

## 功能介绍

通过```ClipboardService```服务，将文本内容置于系统剪切板内

## 使用方法

```csharp
    [Inject]
    [NotNull]
    private ClipboardService? ClipboardService { get; set; }

    private string content { get; set; } = "Hello BootstrapBlazor";

    private async Task Copy()
    {
        await ClipboardService.Copy(content);
    }
```

## 重要提示

请注意，只能在HTTPS安全连接下运行，或者在本地localhost开发环境中使用。
