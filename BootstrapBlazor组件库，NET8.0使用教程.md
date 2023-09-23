# BootstrapBlazor组件库，NET8.0使用教程

```BootstrapBlazor```组件库官网 <https://www.blazor.zone/components>

```BootstrapBlazor```组件库github仓库地址 <https://github.com/dotnetcore/BootstrapBlazor>

```BootstrapBlazor```组件库gitee仓库地址 <https://gitee.com/LongbowEnterprise/BootstrapBlazor>

1、先创建一个NET8.0 Blazor WebApp项目

## 添加包引用

2、在项目中添加```BootstrapBlazor```和```BootstrapBlazor.FontAwesome```的nuget引用。

![img](https://img2023.cnblogs.com/blog/2902819/202309/2902819-20230923111531912-60764761.png)

```xml
<ItemGroup>
    <PackageReference Include="BootstrapBlazor" Version="7.10.8-beta07" />
    <PackageReference Include="BootstrapBlazor.FontAwesome" Version="7.5.0" />
</ItemGroup>
```

>BlazorServer

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">
 <PropertyGroup>
  <TargetFramework>net8.0</TargetFramework>
  <Nullable>enable</Nullable>
  <ImplicitUsings>enable</ImplicitUsings>
 </PropertyGroup>

 <ItemGroup>
  <ProjectReference Include="..\BlazorApp1.Client\BlazorApp1.Client.csproj" />
  <PackageReference Include="Microsoft.AspNetCore.Components.WebAssembly.Server" Version="8.0.0-rc.1.23421.29" />
 </ItemGroup>

 <ItemGroup>
  <PackageReference Include="BootstrapBlazor" Version="7.10.8-beta07" />
  <PackageReference Include="BootstrapBlazor.FontAwesome" Version="7.5.0" />
 </ItemGroup>
</Project>
```

>BlazorWebAssembly

```xml
<Project Sdk="Microsoft.NET.Sdk.BlazorWebAssembly">
 <PropertyGroup>
  <TargetFramework>net8.0</TargetFramework>
  <ImplicitUsings>enable</ImplicitUsings>
  <Nullable>enable</Nullable>
  <NoDefaultLaunchSettingsFile>true</NoDefaultLaunchSettingsFile>
  <StaticWebAssetProjectMode>Default</StaticWebAssetProjectMode>
 </PropertyGroup>

 <ItemGroup>
  <PackageReference Include="Microsoft.AspNetCore.Components.WebAssembly" Version="8.0.0-rc.1.23421.29" />
 </ItemGroup>

 <ItemGroup>
  <PackageReference Include="BootstrapBlazor" Version="7.10.8-beta07" />
  <PackageReference Include="BootstrapBlazor.FontAwesome" Version="7.5.0" />
 </ItemGroup>
</Project>
```

3、在```App.razor```文件中导入```BootstrapBlazor```组件库的```css```和```JavaScript```引用。

## 添加CSS引用

```css``` 引用一定要放在```<link href="css/site.css" rel="stylesheet" />```这行代码上面

``` html
<!-- 引用 BootstrapBlazor.FontAwesome 字体库包 !-->
<link href="_content/BootstrapBlazor.FontAwesome/css/font-awesome.min.css" rel="stylesheet">
<!-- 引用 BootstrapBlazor 组件库包 !-->
<link href="_content/BootstrapBlazor/css/bootstrap.blazor.bundle.min.css" rel="stylesheet">
```

## 添加JavaScript引用

```html
<script src="_content/BootstrapBlazor/js/bootstrap.blazor.bundle.min.js"></script>
```

![img](https://img2023.cnblogs.com/blog/2902819/202309/2902819-20230923112038995-518119751.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
    <base href="/" />

    <!-- 删除下面这行bootstrap默认引用 !-->
    <!-- <link rel="stylesheet" href="bootstrap/bootstrap.min.css" />!-->
    <!-- 引用 BootstrapBlazor.FontAwesome 字体库包 !-->
    <link href="_content/BootstrapBlazor.FontAwesome/css/font-awesome.min.css" rel="stylesheet">
    <!-- 引用 BootstrapBlazor 组件库包 !-->
    <link href="_content/BootstrapBlazor/css/bootstrap.blazor.bundle.min.css" rel="stylesheet">

    <link rel="stylesheet" href="app.css" />
    <link rel="stylesheet" href="BlazorApp1.styles.css" />
    <link rel="icon" type="image/png" href="favicon.png" />
    <HeadOutlet />
</head>

<body>
    <Routes />
    <script src="_framework/blazor.web.js"></script>
    <!-- 引用 BootstrapBlazor 组件库包 !-->
    <script src="_content/BootstrapBlazor/js/bootstrap.blazor.bundle.min.js"></script>
</body>

</html>
```

## 添加```BootstrapBlazor```服务

4、接下来在```Program.cs```中添加这行代码：```builder.Services.AddBootstrapBlazor();```

```csharp
using BlazorApp1.Components;

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddRazorComponents()
    .AddServerComponents()
    .AddWebAssemblyComponents();

//AddBootstrapBlazor
builder.Services.AddBootstrapBlazor();

var app = builder.Build();

if (app.Environment.IsDevelopment())
{
    app.UseWebAssemblyDebugging();
}
else
{
    app.UseExceptionHandler("/Error");
    app.UseHsts();
}

app.UseHttpsRedirection();

app.UseStaticFiles();

app.MapRazorComponents<App>()
    .AddServerRenderMode()
    .AddWebAssemblyRenderMode();

app.Run();
```

## 添加```_Imports.razor```全局引用

5、打开```_Imports.razor```文件，导入```BootstrapBlazor```组件库：```@using BootstrapBlazor.Components```

```html
@using System.Net.Http
@using System.Net.Http.Json
@using Microsoft.AspNetCore.Components.Forms
@using Microsoft.AspNetCore.Components.Routing
@using Microsoft.AspNetCore.Components.Web
@using Microsoft.AspNetCore.Components.Web.Virtualization
@using Microsoft.JSInterop
@using BlazorApp1
@using BlazorApp1.Components
@using BootstrapBlazor.Components
```

## 添加```BootstrapBlazorRoot```组件

6、接下最后一步，在```Routes.razor```文件中添加```<BootstrapBlazorRoot>```根组件。

```html
<BootstrapBlazorRoot>
    <Router AppAssembly="@typeof(App).Assembly" 
            AdditionalAssemblies="new[] { typeof(Client._Imports).Assembly }">
        <Found Context="routeData">
            <RouteView RouteData="@routeData" DefaultLayout="@typeof(Layout.MainLayout)" />
            <FocusOnNavigate RouteData="@routeData" Selector="h1" />
        </Found>
    </Router>
</BootstrapBlazorRoot>
```

完成以上步骤后，就可以愉快的使用```BootstrapBlazor```组件库啦！

![img](https://img2023.cnblogs.com/blog/2902819/202309/2902819-20230923134228017-679945502.png)
