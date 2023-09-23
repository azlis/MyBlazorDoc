# BootstrapBlazor组件库，Table组件导出选中行数据

## 问题描述

有很多小伙伴在使用```BootstrapBlazor```组件库的```Table```组件导出功能时，不知道怎么通过外部按钮来导出数据。

![img](https://img2023.cnblogs.com/blog/2902819/202309/2902819-20230922164505142-143122976.png)

## 解决方案

通过```@ref```当前表格对象来获取数据，然后进行导出操作。

Razor代码

```html
<Button class="mb-2" Text="导出Table数据" OnClick="@ExportData" />

<Table @ref=@_table TItem="Foo" IsPagination="true" PageItemsSource="PageItemsSource" class="table-demo"
       IsStriped="true" IsBordered="true" ShowSkeleton="true" IsMultipleSelect="true"
       ShowToolbar="true" ShowSearch="true" ShowExtendButtons="true"
       SelectedRows="@SelectRows"
       OnExportAsync="OnExportAsync"
       AutoGenerateColumns="true"
       EditMode="EditMode.Popup">
    <TableColumns>
        <TableColumn @bind-Field="@context.Hobby" Items="GetHobbys(context)" />
    </TableColumns>
</Table>
```

C#代码

```csharp
[Inject]
[NotNull]
private ITableExcelExport? Exporter { get; set; }

private Table<Foo>? _table;

private async Task ExportData()
{
    if (_table is not null)
    {
        await Exporter.ExportAsync(_table.Rows, _table.Columns, "Test.xlsx");
    }
}
```

## 实现效果

这样就可以根据你自己的布局和页面设计来进行数据的导出操作了。
![img](https://img2023.cnblogs.com/blog/2902819/202309/2902819-20230922164734539-736286660.png)

## 注意事项

```Table```组件的导出功能需要安装独立功能包。
