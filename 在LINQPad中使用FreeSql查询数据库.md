# 如何在LINQPad中使用FreeSql

LINQPad是一款强大的C#交互式编程环境，它可以让你轻松地编写和测试C#代码片段。除了作为一个交互式编程环境，LINQPad还可以用来连接各种数据源，包括SQL数据库、NoSQL数据库、Web服务等等。此外，LINQPad还支持使用NuGet包管理器来安装和管理第三方库。

有时候需要调试某段SQL，但是直接在项目里面编写的话，调试起来不仅麻烦，而且耗时。

那么在LINQPad中，我们可以像在```SQL Server Management Studio Management Studio```中，写SQL一样来写```LINQ```表达式和任何```C#```代码，并且即时编译运行获得结果！

```FreeSql```是一款国产的功能强大的 ```.NET ORM```，在```LINQPad```中是不支持直接使用```FreeSql```的，不过我们可以通过添加自定义拓展类的方法，来调用```FreeSql```。

下面是详细的操作步骤。

1. 打开LINQPad添加一个新的连接
   ![img](https://img2023.cnblogs.com/blog/2902819/202304/2902819-20230413144958164-872393958.png)
2. 这里选择数据上下文的时候一定要选择EFCore！
   ![img](https://img2023.cnblogs.com/blog/2902819/202304/2902819-20230413145036006-950705986.png)
3. 选择你的数据库类型并创建连接
   ![img](https://img2023.cnblogs.com/blog/2902819/202304/2902819-20230413145206940-997109281.png)
4. 回到主界面，按下Shift + Ctrl + Y 快捷键，创建一个自定义拓展，代码如下。

   ```csharp
       public static class free
       {
          public static IFreeSql sql = new FreeSql.FreeSqlBuilder()
                .UseConnectionString(FreeSql.DataType.SqlServer, Util.CurrentCxString)
                .UseMonitorCommand(s => Util.Metatext(s.CommandText).Dump())
                .Build();
       }
   ```

5. 代码中的```Util.CurrentCxString```表示在LINQPad中获取当前上下文的连接字符串。```.UseMonitorCommand(s => Util.Metatext(s.CommandText).Dump())```用于输出```SQL```语句
    ![img](https://img2023.cnblogs.com/blog/2902819/202304/2902819-20230413145540636-1574293253.png)
6. 接下来在查询中使用FreeSql。

   ```csharp
      var result = await free.sql.Select<TABLE>()...
   ```

   ![img](https://img2023.cnblogs.com/blog/2902819/202304/2902819-20230413150156792-1241575351.png)
7. 以上就是关于如何在LINQPad中使用FreeSql的全部内容了。
