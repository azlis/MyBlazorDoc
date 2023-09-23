# BootstrapBlazor 组件库保姆级使用教程

```BootstrapBlazor```组件库官网 <https://www.blazor.zone/components>

```BootstrapBlazor```组件库github仓库地址 <https://github.com/dotnetcore/BootstrapBlazor>

```BootstrapBlazor```组件库gitee仓库地址 <https://gitee.com/LongbowEnterprise/BootstrapBlazor>

1、先创建一个Blazor Server项目

2、在项目中添加```BootstrapBlazor```和```BootstrapBlazor.FontAwesome```nuget包
![img](https://img2023.cnblogs.com/blog/2902819/202305/2902819-20230503140838063-1766869953.png)

![img](https://img2023.cnblogs.com/blog/2902819/202305/2902819-20230503141203276-70035940.png)

![img](https://img2023.cnblogs.com/blog/2902819/202305/2902819-20230503141136777-816767177.png)

3、接下来在```Program.cs```中添加这行代码：```builder.Services.AddBootstrapBlazor();```
![img](https://img2023.cnblogs.com/blog/2902819/202305/2902819-20230503141516387-418918293.png)

4、打开```_Imports.razor```文件，导入```BootstrapBlazor```组件库命名空间：```@using BootstrapBlazor.Components```
![img](https://img2023.cnblogs.com/blog/2902819/202305/2902819-20230503141911479-1643952946.png)

5、接下来打开```Pages```文件夹，打开```_Host.cshtml```文件，添加```css```和```JavaScript```引用

## CSS 引用代码

```css``` 引用一定要放在```<link href="css/site.css" rel="stylesheet" />```这行代码上面

``` html
    <!-- 引用 BootstrapBlazor.FontAwesome 字体库包 !-->
    <link href="_content/BootstrapBlazor.FontAwesome/css/font-awesome.min.css" rel="stylesheet">
    <!-- 引用 BootstrapBlazor 组件库包 !-->
    <link href="_content/BootstrapBlazor/css/bootstrap.blazor.bundle.min.css" rel="stylesheet">
```

## JavaScript 引用代码

```javaScript
    <script src="_content/BootstrapBlazor/js/bootstrap.blazor.bundle.min.js"></script>
```

![img](https://img2023.cnblogs.com/blog/2902819/202305/2902819-20230503142609047-888740727.png)

5、接下最后一步，在```App.razor```文件中添加```<BootstrapBlazorRoot>```组件。

![img](https://img2023.cnblogs.com/blog/2902819/202305/2902819-20230503143151853-1493189410.png)

完成以上步骤后，就可以愉快的使用```BootstrapBlazor```组件库啦！
