# BootstrapBlazor组件库，Table组件外部刷新数据

## 问题描述

有很多小伙伴在使用```BootstrapBlazor```组件库的```Table```组件时，经常会遇到外部调用```OnQueryAsync```的需求。

## 解决方案

我们可以使用```@ref```指令，将当前```Table```对象引用到一个变量上面。

Razor代码
>注意```@ref```指令要写```@```符号

```html
<Button @onclick="Query" Text="查询数据" IsAsync="true" />

<Table @ref=@TestTable TItem="DataList" OnQueryAsync="@OnQueryAsync">
    <TableColumns>
        <TableColumn @bind-Field="@context.日期" />
        <TableColumn @bind-Field="@context.编号" />
        <TableColumn @bind-Field="@context.等级" />
        <TableColumn @bind-Field="@context.规格" />
    </TableColumns>
</Table>
```

C#代码
>注意```<>```内的类型和```TItem```一致

```csharp
private Table<DataList>? TestTable;

private async Task Query()
{
    //通过下面的代码在外部调用Table的QueryAsync刷新数据。
    await TestTable.QueryAsync();
}

private async Task<QueryData<DataList>> OnQueryAsync(QueryPageOptions options)
{
    var Items = await tz.GetDatasAsync(Options);
    return new QueryData<DataList>()
    {
        Items = Items
    };
}
```

## 注意事项

```Table```组件的```Items```和```OnQueryAsync```只能二选一，不能混用！本方案仅适合```OnQuery```模式，```Items```模式请调用```StateHasChanged```。
