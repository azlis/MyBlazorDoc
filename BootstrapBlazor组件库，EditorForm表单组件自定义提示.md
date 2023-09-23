# BootstrapBlazor组件库，EditorForm表单组件自定义提示

## 问题描述

有很多小伙伴在使用```BootstrapBlazor```组件库的```EditorForm```表单组件时，不知道怎么修改提示文本。
![img](https://img2023.cnblogs.com/blog/2902819/202309/2902819-20230922155032699-1965058834.png)

## 解决方案

我们可以修改```PlaceHolder```的值，来修改默认的提示文本信息。

Razor代码

```html
<EditorForm Model="@Model" AutoGenerateAllItem="false">
    <FieldItems>
        <EditorItem @bind-Field="@context.Name" PlaceHolder="用户姓名" />
    </FieldItems>
</EditorForm>
```

## 实现效果

![img](https://img2023.cnblogs.com/blog/2902819/202309/2902819-20230922155140258-2112023185.png)

## 注意事项

```PlaceHolder```的默认值为,"```请输入...```"，如果不想要提示文本，设置为空即可。
