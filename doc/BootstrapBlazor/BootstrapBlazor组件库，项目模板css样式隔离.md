# BootstrapBlazor组件库，项目模板css样式隔离问题

## 问题描述

有很多小伙伴在使用```BootstrapBlazor```组件库的项目模板的时候，遇到了隔离样式不生效的问题。

## 解决方案

只需要添加一行代码即可解决问题。

```html
    <link href="xxx.styles.css" rel="stylesheet" />
```

1. 在项目解决方案中，找到这两个文件。

    ![img](https://img2023.cnblogs.com/blog/2902819/202309/2902819-20230922091941259-1700773323.png)

2. 在```Server```项目中```Pages/_Layout.cshtml```文件中的```head```添加代码。

    ![img](https://img2023.cnblogs.com/blog/2902819/202309/2902819-20230922092132191-1024478568.png)

    ```html
    <head>
        <meta charset="utf-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <base href="~/" />
        <link rel="stylesheet" href="libs/font-awesome/css/font-awesome.min.css">
        <link rel="stylesheet" href="_content/BootstrapBlazor/css/bootstrap.blazor.bundle.min.css">
        <link rel="stylesheet" href="_content/BootstrapBlazor/css/motronic.min.css">
        <link rel="stylesheet" href="_content/BootstrapBlazorApp1.Shared/css/site.css">
        <link rel="stylesheet" href="_content/BootstrapBlazorApp1.Shared/css/motronic.css">

        <!-- 添加下面这行代码 -->
        <link href="BootstrapBlazorApp1.styles.css" rel="stylesheet" />
        <!-- 添加上面这行代码 -->

        <title>Bootstrap Blazor Server App</title>
        <component type="typeof(HeadOutlet)" render-mode="ServerPrerendered" />
    </head>
    ```

3. 在```WebAssembly```项目中```wwwroot/index.html```文件中的```head```添加代码。
    ![img](https://img2023.cnblogs.com/blog/2902819/202309/2902819-20230922092456233-754462574.png)

    ```html
    <head>
        <meta charset="utf-8">
        <title>Bootstrap Blazor Wasm App</title>
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0, shrink-to-fit=no">
        <meta content="bootstrap,blazor,wasm,webassembly,UI,netcore,web,assembly" name="Keywords">
        <base href="/">
        <link rel="icon" href="favicon.ico" type="image/x-icon">
        <link rel="shortcut icon" href="favicon.ico" type="image/x-icon">
        <link rel="apple-touch-icon" href="icon-512.png">
        <link rel="manifest" href="manifest.json">
        <link rel="stylesheet" href="libs/font-awesome/css/font-awesome.min.css">
        <link rel="stylesheet" href="_content/BootstrapBlazor/css/bootstrap.blazor.bundle.min.css">
        <link rel="stylesheet" href="_content/BootstrapBlazorApp1.Shared/css/site.css">
        <link rel="stylesheet" href="_content/BootstrapBlazorApp1.Shared/css/motronic.css">

        <!-- 添加下面这行代码 -->
        <link href="BootstrapBlazorApp1.styles.css" rel="stylesheet" />
        <!-- 添加上面这行代码 -->

        <link rel="stylesheet" href="style/loading.css">
    </head>
    ```

## 注意事项

引用中的```xxx.styles.css```，xxx表示你当前的项目名称。
