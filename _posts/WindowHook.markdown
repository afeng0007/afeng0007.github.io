WindowHook:
----

### 说明：
钩子是在系统的消息循环中添加自己的处理函数的方法：钩子能够处理交互事件：例如：消息，鼠标事件、键盘事件，钩子能够在它收到事件，并且能够修改、或者丢弃这些事件。一个钩子处理函数可以处理收到的钩子事件也可以修改或者丢弃这些事件。

根据调用方式的不同可以分为：`SetWindowsHookEx`加载到进程内的钩子，`SetWinEventHook`既可以加载到进程内又可以在进程外接收，区别在于：

* `SetWindowsHookEx`只有进程内钩子，没有进程外钩子，意味着如果要在64位系统中正确获取通知的话必须提供64bit和32bit的dll。而且要求加载的程序也是对应的版本。而`SetWinEventHook`既可以是进程内钩子，也可以是进程外钩子。如果是进程内钩子和`SetWindowsHookEx`的要求类似，对于64bit系统要求针对不同的进程加载不同版本的dll.
* `SetWindowsHookEx`用于获取`WM_`开头的消息类型，而`SetWinEventHook`用于获取`EVENT_`开头的消息类型。

### 钩子的应用场景：
* 监视某些消息。
* 提供录制和回放的处理宏。
* 提供F1帮助。
* 模拟鼠标或者键盘输入。

#### 注意事项:
* 钩子的处理会影响系统性能。只有在必要的时候才添加钩子，并且要尽快释放掉钩子。

### 钩子类型类型：
`SetWindowsHookEx`:   
函数原型`HHOOK WINAPI SetWindowsHookEx(_In_ int idHook, _In_ HOOKPROC lpfn, _In_ HINSTANCE hMod, _In_ DWORD dwThreadId);`   
其中的idHook是函数原型。有以下几种类型:   

* WH_CALLWNDPROC 和 WH_CALLWNDPROCRET:用于监视发送到窗口的消息。
* WH_CBT: 系统会调用CBT钩子在activating， creating， destroying， minimizing， maximizing， moving or sizing window.
* WH_DEBUG: 系统在调用其他hook之前都会调用这种Hook。应该是一种Hook的debug。
* WH_FOREGROUNDIDLE： 前端线程是空闲状态的时候会调用这类Hook。
* WH_GETMESSAGE： 在GetMessage和PeekMessage return之前调用这类hook。这个Hook能够监听Mouse和keyboard的消息。
* WH_JOURNALPLAYBACK： 用于向系统消息队列中插入消息。使用这种Hook能够回放系统消息。这个钩子是一种全局钩子，不能指定threadid。
* WH_JOURNALRECORD： 用于记录和监视输入事件，能够用来记录事件。
* WH_KEYBOARD_LL: 用于监视键盘输入。
* WH_KEYBOARD: 用于监视键盘消息WM_KEYDOWN和WM_KEYUP的消息。
* WH_MOUSE_LL: 用于监视鼠标输入。
* WH_MOUSE: 用于监视鼠标消息处理WH_MOUSE.
* WH_MSGFILTER: 用于监视menu，scroll bar或者dlg box。
* WH_SHELL: 顶层窗口activate或者顶层窗口被创建或者销毁。

`SetWinEventHook`:
函数原型:`HWINEVENTHOOK WINAPI SetWinEventHook(_In_ UINT eventMin, _In_ UINT eventMax, HMODULE hmodWinEventProc, WINEVENTPROC lpfnWinEventProc, DWORD idProcess, DWORD idThread, UINT dwflags);`

如前所述，`SetWinEventHook`既可以挂载进程内钩子，也可以挂载进程外钩子。

### 钩子注入需要注意的问题：
32bit的程序可以加载32bit的dll用来注入32bit的hook。对于64bit的程序，需要使用64bit的程序进行加载。

### 钩子链：
系统提供了很多不同类型的钩子，每种类型提供了对消息处理机制的不同方便的访问。系统对于不同类型的钩子提供不同的钩子链。

### 钩子处理函数:
为了有效处理某些类型的钩子，可以使用`SetWindowsHookEx`来加载这些钩子.全局的钩子监视所有线程的消息。特定线程的消息钩子监视特定线程的钩子。**全局钩子只应该应用于debug目的**
