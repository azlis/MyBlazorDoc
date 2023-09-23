# BootstrapBlazor组件库调用浏览器全局事件

有时候blazor开发的时候可能会使用一些浏览器的全局事件，但是blazor默认没有提供相关的方法去调用，只能通过js。

```BootstrapBlazor```组件库为我们提供了封装好的方法可以很方便的去调用。

```csharp
[Inject]
[NotNull]
private IJSRuntimeEventHandler? JSRuntimeEventHandler { get; set; }

protected override async Task OnAfterRenderAsync(boolfirstRender)
{
    if (firstRender)
    {
        await JSRuntimeEventHandler.RegisterEvent(DOMEvents.Scroll);
        JSRuntimeEventHandler.OnScroll += OnScroll;
    }
}

private async void OnScroll()
{
    await ...
}

```

这样就成功订阅了一个浏览器的全局滚动事件

下面是支持的事件列表

```csharp
public enum DOMEvents
{
    /// <summary>
    /// Click 事件枚举
    /// </summary>
    [Description("click")]
    Click,
    /// <summary>
    /// Dblclick 事件枚举
    /// </summary>
    [Description("dblclick")]
    Dblclick,
    /// <summary>
    /// Mouseup 事件枚举
    /// </summary>
    [Description("mouseup")]
    Mouseup,
    /// <summary>
    /// Mousedown 事件枚举
    /// </summary>
    [Description("mousedown")]
    Mousedown,
    /// <summary>
    /// Contextmenu 事件枚举
    /// </summary>
    [Description("contextmenu")]
    Contextmenu,
    /// <summary>
    /// Mousewheel 事件枚举
    /// </summary>
    [Description("mousewheel")]
    Mousewheel,
    /// <summary>
    /// DOMMouseScroll 事件枚举
    /// </summary>
    [Description("dOMMouseScroll")]
    DOMMouseScroll,
    /// <summary>
    /// Mouseover 事件枚举
    /// </summary>
    [Description("mouseover")]
    Mouseover,
    /// <summary>
    /// Mouseout 事件枚举
    /// </summary>
    [Description("mouseout")]
    Mouseout,
    /// <summary>
    /// Mousemove 事件枚举
    /// </summary>
    [Description("mousemove")]
    Mousemove,
    /// <summary>
    /// Selectstart 事件枚举
    /// </summary>
    [Description("selectstart")]
    Selectstart,
    /// <summary>
    /// Selectend 事件枚举
    /// </summary>
    [Description("selectend")]
    Selectend,
    /// <summary>
    /// Keydown 事件枚举
    /// </summary>
    [Description("keydown")]
    Keydown,
    /// <summary>
    /// Keypress 事件枚举
    /// </summary>
    [Description("keypress")]
    Keypress,
    /// <summary>
    /// Keyup 事件枚举
    /// </summary>
    [Description("keyup")]
    Keyup,
    /// <summary>
    /// Orientationchange 事件枚举
    /// </summary>
    [Description("orientationchange")]
    Orientationchange,
    /// <summary>
    /// Touchstart 事件枚举
    /// </summary>
    [Description("touchstart")]
    Touchstart,
    /// <summary>
    /// Touchmove 事件枚举
    /// </summary>
    [Description("touchmove")]
    Touchmove,
    /// <summary>
    /// Touchend 事件枚举
    /// </summary>
    [Description("touchend")]
    Touchend,
    /// <summary>
    /// Touchcancel 事件枚举
    /// </summary>
    [Description("touchcancel")]
    Touchcancel,
    /// <summary>
    /// Pointerdown 事件枚举
    /// </summary>
    [Description("pointerdown")]
    Pointerdown,
    /// <summary>
    /// Pointermove 事件枚举
    /// </summary>
    [Description("pointermove")]
    Pointermove,
    /// <summary>
    /// Pointerup 事件枚举
    /// </summary>
    [Description("pointerup")]
    Pointerup,
    /// <summary>
    /// Pointerleave 事件枚举
    /// </summary>
    [Description("pointerleave")]
    Pointerleave,
    /// <summary>
    /// Pointercancel 事件枚举
    /// </summary>
    [Description("pointercancel")]
    Pointercancel,
    /// <summary>
    /// Gesturestart 事件枚举
    /// </summary>
    [Description("gesturestart")]
    Gesturestart,
    /// <summary>
    /// Gesturechange 事件枚举
    /// </summary>
    [Description("gesturechange")]
    Gesturechange,
    /// <summary>
    /// Gestureend 事件枚举
    /// </summary>
    [Description("gestureend")]
    Gestureend,
    /// <summary>
    /// Focus 事件枚举
    /// </summary>
    [Description("focus")]
    Focus,
    /// <summary>
    /// Blur 事件枚举
    /// </summary>
    [Description("blur")]
    Blur,
    /// <summary>
    /// Change 事件枚举
    /// </summary>
    [Description("change")]
    Change,
    /// <summary>
    /// Reset 事件枚举
    /// </summary>
    [Description("reset")]
    Reset,
    /// <summary>
    /// Select 事件枚举
    /// </summary>
    [Description("select")]
    Select,
    /// <summary>
    /// Submit 事件枚举
    /// </summary>
    [Description("submit")]
    Submit,
    /// <summary>
    /// Focusin 事件枚举
    /// </summary>
    [Description("focusin")]
    Focusin,
    /// <summary>
    /// Focusout 事件枚举
    /// </summary>
    [Description("focusout")]
    Focusout,
    /// <summary>
    /// Load 事件枚举
    /// </summary>
    [Description("load")]
    Load,
    /// <summary>
    /// Unload 事件枚举
    /// </summary>
    [Description("unload")]
    Unload,
    /// <summary>
    /// Beforeunload 事件枚举
    /// </summary>
    [Description("beforeunload")]
    Beforeunload,
    /// <summary>
    /// Resize 事件枚举
    /// </summary>
    [Description("resize")]
    Resize,
    /// <summary>
    /// Move 事件枚举
    /// </summary>
    [Description("move")]
    Move,
    /// <summary>
    /// DOMContentLoaded 事件枚举
    /// </summary>
    [Description("dOMContentLoaded")]
    DOMContentLoaded,
    /// <summary>
    /// Readystatechange 事件枚举
    /// </summary>
    [Description("readystatechange")]
    Readystatechange,
    /// <summary>
    /// Error 事件枚举
    /// </summary>
    [Description("error")]
    Error,
    /// <summary>
    /// Abort 事件枚举
    /// </summary>
    [Description("abort")]
    Abort,
    /// <summary>
    /// Scroll 事件枚举
    /// </summary>
    [Description("scroll")]
    Scroll
}
```
