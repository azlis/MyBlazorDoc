# BootstrapBlazor组件库，Table组件导出选中行数据

## 问题描述

有很多小伙伴在使用```BootstrapBlazor```组件库的```Table```组件导出功能时，不知道怎么导出选中的行数据。

![img](https://img2023.cnblogs.com/blog/2902819/202309/2902819-20230922162219303-1730977539.png)

## 解决方案

通过```SelectedRows```来导出选中的行数据。

Razor代码

```html
<Table TItem="Foo" IsPagination="true" PageItemsSource="PageItemsSource" class="table-demo"
       IsStriped="true" IsBordered="true" ShowSkeleton="true" IsMultipleSelect="true"
       ShowToolbar="true" ShowSearch="true" ShowExtendButtons="true" ShowExportButton="true"
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

private List<Foo> SelectRows { get; set; } = new List<Foo>();

private async Task<bool> OnExportAsync(ITableExportDataContext<Foo> context)
{
    return await Exporter.ExportAsync(SelectRows, context.Columns, "Test.xlsx");
}
```

## 实现效果

![img](https://img2023.cnblogs.com/blog/2902819/202309/2902819-20230922162310588-1692928726.png)

## 不导出选中行数据

C#代码

```csharp
[Inject]
[NotNull]
private ITableExcelExport? Exporter { get; set; }

private List<Foo> SelectRows { get; set; } = new List<Foo>();

private async Task<bool> OnExportAsync(ITableExportDataContext<Foo> context)
{
    return await Exporter.ExportAsync(context.Rows.Except(SelectRows), context.Columns, "Test.xlsx");
}
```

![img](https://img2023.cnblogs.com/blog/2902819/202309/2902819-20230922162920881-715466646.png)

## 注意事项

```Table```组件的导出功能需要安装独立功能包。
