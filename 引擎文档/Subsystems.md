Any Object can be registered to the Context as a subsystem, by using the function RegisterSubsystem(). They can then be accessed by any other Object inside the same context by calling GetSubsystem(). Only one instance of each object type can exist as a subsystem.

After Engine initialization, the following subsystems will always exist:

Time: manages frame updates, frame number and elapsed time counting, and controls the frequency of the operating system low-resolution timer.
WorkQueue: executes background tasks in worker threads.
FileSystem: provides directory operations.
Log: provides logging services.
ResourceCache: loads resources and keeps them cached for later access.
Network: provides UDP networking and scene replication.
Input: handles keyboard and mouse input. Will be inactive in headless mode.
UI: the graphical user interface. Will be inactive in headless mode.
Audio: provides sound output. Will be inactive if sound disabled.
Engine: creates the other subsystems and controls the main loop iteration and framerate limiting.
The following subsystems are optional, so GetSubsystem() may return null if they have not been created:

Profiler: Provides hierarchical function execution time measurement using the operating system performance counter. Exists if profiling has been compiled in (configurable from the root CMakeLists.txt)
Graphics: Manages the application window, the rendering context and resources. Exists if not in headless mode.
Renderer: Renders scenes in 3D and manages rendering quality settings. Exists if not in headless mode.
Script: Provides the AngelScript execution environment. Needs to be created and registered manually.
Console: provides an interactive AngelScript console and log display. Created by calling CreateConsole().
DebugHud: displays rendering mode information and statistics and profiling data. Created by calling CreateDebugHud().
In script, the subsystems are available through the following global properties: time, fileSystem, log, cache, network, input, ui, audio, engine, graphics, renderer, script, console, debugHud. Note that WorkQueue and Profiler are not available to script due to their low-level nature.


任何对象都可以通过RegisterSubsystem()方法，作为一个子系统(subsytem)注册到Context中。然后该Context下的所有对象都能通过GetSubsystem()方法来获得这个注册过的对象了，同种类型只能注册一个对象作为子系统(单例)。

在引擎初始化之后，以下的子系统将会被生成：

Time: 管理帧事件、帧数、消耗时间的计算以及控制(操作系统低分辨率)计时器的频率。
WorkQueue: 负责开启工作线程，用来执行一些后台任务。
FileSystem: 文件系统操作。
Log: 提供了日志服务。
ResourceCache: 负责读取资源以及缓存资源。
Network: 提供了UDP和场景复制。
Input: 处理键盘和鼠标事件，在headless模式下会无效。
UI: 用户图形界面，在headless模式下会无效。
Audio: 负责声音输出，在SOUND宏被关闭的情况下，会无效。
Engine: 创建其他的子系统，控制主循环和帧率限制。

以下的子系统是可选择的，如果它们没有创建，那么GetSubsytem()会返回null。

Profiler: 通过使用系统性能计数器，提供了一些分层的函数来进行执行时间的测量，该子系统仅当profiling被编译进去时才会存在(通过CMakeLists.txt配置)。
Graphics: 管理应用窗口，渲染上下文以及资源。在headless模式未开启时存在。
Renderer: 负责渲染3D场景，并且管理渲染的质量，在headless模式未开启时存在。
Script: 提供了AngelScript的执行环境，需要手动创建和注册。
Console: 提供了与AngleScript交互的控制台以及日志功能。通过CreateConsole()创建。
DebugHud: 显示渲染模式的信息和统计，以及剖面数据。通过CreateDebugHud()来创建。

在脚本中，子系统可以通过全局的属性: time, fileSystem, log, cache, network, input, ui, audio, engine, graphics, renderer, script, console, debugHud来访问。需要注意的是由于WorkQueue和Profiler的底层特性，它们在脚本中是不能使用的。