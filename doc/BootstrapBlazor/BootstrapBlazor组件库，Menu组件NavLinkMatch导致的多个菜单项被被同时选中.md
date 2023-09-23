# BootstrapBlazor组件库，Menu组件NavLinkMatch导致的多个菜单项被被同时选中

BootstrapBlazor版本更新到7.9.0后，Menu组件出现首页同时被选中的情况

![img](https://img2023.cnblogs.com/blog/2902819/202308/2902819-20230805092915947-24017457.png)

默认首页```/```路径是选中状态，但是当选中其他路径后，首页路径还是选中状态。
这是因为在BootstrapBlazor组件最新版中支持了一个新特性。可以在路径后面添加#xxx这种格式
默认情况下是```NavLinkMatch.Prefix```，要解决这个问题很简单，只需要单独把首页```/```修改为```NavLinkMatch.All```就可以了

>razor代码

```html
<Menu Items="@_menuItems" IsVertical="true" />
```

>C#代码

```csharp

private List<MenuItem>? _menuItems;

protected override async Task OnInitializedAsync()
{
    await base.OnInitializedAsync();
    _menuItems = CreateMenuItems(Menu.Where(x => x.Roles!.Any(y => y.Id == RoleId)).OrderBy(x => x.Seq).ToList(), 0);
}

private List<MenuItem> CreateMenuItems(List<Menu> menus, int parentId)
{
    var selectedMenus = new List<MenuItem>();
    var selectedMenuEntities = menus.Where(x => x.ParentId == parentId).ToList();
    foreach (var menuEntity in selectedMenuEntities)
    {
        var menuItem = new MenuItem(menuEntity.Name!, menuEntity.Url, menuEntity.Icon)
        {
            Items = CreateMenuItems(menus, menuEntity.Id)
        };
        //判断是否首页
        if (menuItem.Url == "/")
        {
            //需要引入命名空间:Microsoft.AspNetCore.Components.Routing
            menuItem.Match = NavLinkMatch.All;
        }
        selectedMenus.Add(menuItem);
    }
    return selectedMenus;
}
```

Menu组件在使用中需要特别注意NavLinkMatch.Prefix和NavLinkMatch.All的区别，要不然就会出现多个菜单项被同时选中的情况。