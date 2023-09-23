# BootstrapBlazor组件库更优雅的调用js方法

在blazor开发中，有时候需要去调用js代码来处理一些逻辑。使用BootstrapBlazor组件库自带的```JSModuleAutoLoader```特性可以帮助我们更加方便、简洁的去调用js

下面我们用```Live2DDisplay```这个组件为例

我们首先在razor文件中继承接口

>@inherits BootstrapModuleComponentBase

然后引入特性,注意！这里要引用完整的js文件路径！

>@attribute [JSModuleAutoLoader("./_content/BootstrapBlazor.Live2DDisplay/Components/Live2DDisplay/Live2DDisplay.razor.js", AutoInvokeInit = false, JSObjectReference = true, AutoInvokeDispose = false)]

因为涉及到传参，我们需要重写```InvokeInitAsync```方法，如果不需要传参，可以把```AutoInvokeInit```设置为```true```,这样会自动调用```init```方法，就不用去重写了。

```csharp
protected override async Task InvokeInitAsync()
{
    await InvokeVoidAsync("init", Id);
}
```

需要注意的是```JSModuleAutoLoader```默认是调用```init```方法

```js
export function init(id) {
    //...
}
```
