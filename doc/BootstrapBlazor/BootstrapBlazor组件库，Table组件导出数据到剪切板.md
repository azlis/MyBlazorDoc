# BootstrapBlazor组件库，Table组件导出数据到剪切板

## 解决方案

使用```ClipboardService```将```Table```数据导出到剪切板中,并且可以直接粘贴到Excel。

这里我直接采用```ExportButtonDropdownTemplate```添加了2个新的导出选项，一个是导出当前页，一个是导出所有页。

Razor代码

```html
<Table TItem="Foo"
       IsPagination="true" PageItemsSource="@PageItemsSource"
       IsStriped="true" IsBordered="true" IsMultipleSelect="true"
       ShowToolbar="true" ShowDefaultButtons="false" ShowExportButton="true"
       OnQueryAsync="@OnQueryAsync">
    <TableColumns>
        <TableColumn @bind-Field="@context.DateTime" Width="180" />
        <TableColumn @bind-Field="@context.Name" Width="100" />
        <TableColumn @bind-Field="@context.Address" />
        <TableColumn @bind-Field="@context.Count" />
    </TableColumns>
    <ExportButtonDropdownTemplate Context="ExportContext">
        <div class="dropdown-item" @onclick="() => CliBoardExportAsync(ExportContext)">
            <i class="fa-regular fa-file-excel"></i>
            <span>导出当前页数据到剪切板</span>
        </div>
        <div class="dropdown-item" @onclick="() => CliBoardExportAllAsync(ExportContext)">
            <i class="fa-regular fa-file-excel"></i>
            <span>导出所有页数据到剪切板</span>
        </div>
    </ExportButtonDropdownTemplate>
</Table>
```

C#代码

```csharp
    [Inject]
    [NotNull]
    private ITableExcelExport? Exporter { get; set; }

    [Inject]
    [NotNull]
    private ClipboardService? ClipboardService { get; init; }

    private async Task ToClipBoard( IEnumerable<ITableColumn> columns, IEnumerable<Foo> rows)
    {
        var tableColumns = columns.ToList();
        var fieldNames = tableColumns.Select(x => x.GetFieldName()).ToArray();
        var titles = tableColumns.Select(x => x.GetDisplayName()).ToArray();

        var sb = new StringBuilder();
        sb.AppendJoin('\t',titles).AppendLine();

        foreach (var row in rows)
        {
            var values = fieldNames.Select(x => row.GetType().GetProperty(x)?.GetValue(row)).ToArray();
            sb.AppendJoin('\t',values).AppendLine();
        }

        var result = sb.ToString();
        await ClipboardService.Copy(result);
    }

    private async Task CliBoardExportAsync(ITableExportContext<Foo> context)
    {
        await ToClipBoard(context.Columns,context.Rows);
        await ShowToast(true);
    }

    private async Task CliBoardExportAllAsync(ITableExportContext<Foo> context)
    {
        var option = context.BuildQueryPageOptions();
        var filter = option.ToFilter();
        var data = Items.Where(filter.GetFilterFunc<Foo>());
        await ToClipBoard(context.Columns,data);
        await ShowToast(true);
    }
```

## 实现效果

![实现效果](https://img2023.cnblogs.com/blog/2902819/202310/2902819-20231028093004482-1333984307.gif)

## 注意事项

没有注意事项O(∩_∩)O
