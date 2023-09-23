# BootstrapBlazor组件库，组件方法的表达式传参

有时候我们在循环中创建组件的时候，可能想把item的值也一并传入组件的方法事件中去处理，有很多小伙伴就不知道如何去调用事件了。

下面是一段实例代码，通过循环遍历来创建图片，并且创建一个删除图片的按钮，这个按钮的```OnConfirm```方法需要把图片本身也给带进去。
这个时候就可以使用表达式来传参```OnConfirm="@(async()=>await DeleteImages(img))"```。

```html
@foreach (var img in images)
{
    <div class="col-auto">
        <Card IsShadow="true">
            <HeaderTemplate>
                <div class="container">
                    <div class="row">
                        <div class="col-auto">
                            <PopConfirmButton Placement="Placement.Top"
                                              Color="Color.Danger" Size="Size.ExtraSmall"
                                              ConfirmIcon="fa-solid fa-triangle-exclamation text-danger"
                                              ConfirmButtonColor="Color.Danger"
                                              Text="删除照片"
                                              Content="是否确认删除？"
                                              IsAsync="true"
                                              OnBeforeClick="OnBeforeDeleteImages"
                                              OnConfirm="@(async()=>await DeleteImages(img))" />
                        </div>
                        <div class="col-auto">
                            <code>@img.FileNum</code>
                        </div>
                    </div>
                </div>
            </HeaderTemplate>
            <BodyTemplate>
                <ImageViewer style="width:150px;"
                             Alt="@img.Test"
                             Url="@img.Url"
                             PreviewList="@(new List<string>() { img.Url! })"
                             ShowPlaceHolder="true" />
            </BodyTemplate>
        </Card>
    </div>
}
```

```csharp
private async Task DeleteImages(Images image)
{
    await ...
}
```

这样我们就实现了这么一个需求，那如果我需要在传参的同时把组件本身的参数也给传过去，可以用下面的语法

```csharp
OnConfirm="@(async(x)=>await DeleteImages(x,img))"

private async Task DeleteImages(object sender,Images image)
{
    await ...
}
```

表达式括号里面的x,就是组件本身的参数了，这样就实现了组件传参的一个灵活性。
