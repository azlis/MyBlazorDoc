# BlazorServerCookieLogin

## 基于BlazorServer模式实现Cookie登录

### Demo在GitHub:<https://github.com/azlis/BlazorCookieLogin>

### 本次主要使用了```BootstrapBlazor```组件库，和```FreeSql```ORM组件，登录页面主要使用MVC模式来实现，通过前端Login页面发起登陆请求，后端controller控制器返回登录状态

### 我们先看一下项目结构![s1](https://img2023.cnblogs.com/blog/2902819/202306/2902819-20230604230252145-1805813358.png)

### 在Program.cs文件中添加以下关键内容

 ```csharp
builder.Services.AddControllersWithViews();
builder.Services.AddAuthentication(CookieAuthenticationDefaults.AuthenticationScheme).AddCookie();
builder.Services.AddHttpContextAccessor();

app.UseAuthentication();
app.UseAuthorization();
app.MapControllers();
app.MapDefaultControllerRoute();
 ```
