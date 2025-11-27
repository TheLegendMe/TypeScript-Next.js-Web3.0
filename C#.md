| 天数   | 目标                          | 核心内容 + 当天必做的小项目（带完整代码）                    |
| ------ | ----------------------------- | ------------------------------------------------------------ |
| Day 1  | C#语法秒杀                    | 变量、集合、LINQ、null安全、记录、模式匹配 项目：命令行TodoList（支持增删改查+文件保存） |
| Day 2  | 面向对象进阶                  | record、init、with、密封类、partial、源生成器 项目：深拷贝工具（支持循环引用，JSON + 二进制对比） |
| Day 3  | 异步编程彻底掌握              | async/await、Task、ValueTask、IAsyncEnumerable、取消令牌 项目：高并发图片下载器（1000张同时下，支持进度+取消） |
| Day 4  | 委托、事件、Lambda、表达式树  | Func/Action、事件、事件总线、动态LINQ 项目：轻量事件总线 EventBus（发布/订阅，支持异步） |
| Day 5  | .NET 8 现代特性               | Primary Constructor、集合表达式、拦截器、冻结集合 项目：迷你DI容器（支持单例、瞬态、属性注入） |
| Day 6  | Unity实战Day1（C#最常见场景） | MonoBehaviour生命周期、协程 vs async、ScriptableObject、DOTS基础 项目：简易《吸血鬼幸存者》核心（自动攻击+经验球吸取） |
| Day 7  | Unity实战Day2                 | Addressables、Object Pool、UI Toolkit、Animator Override 项目：完成可玩的《吸血鬼幸存者》Demo（3武器+升级） |
| Day 8  | .NET后端快速上手              | ASP.NET Core Minimal API、EF Core Code-First、JWT认证 项目：带登录的Todo API（SQLite + Swagger） |
| Day 9  | 性能与内存极致                | Span<T>、Memory<T>、Stackalloc、ref struct、对象池 项目：超高性能CSV解析器（比StreamReader快5倍） |
| Day 10 | 综合大项目 + 简历包装         | 任选其一： 1. 完整Unity 3D动作游戏Demo（第三人称+连招） 2. WPF + EF Core 桌面工具（资源打包器） 3. 微服务网关（Yarp + Polly） |

每天必背代码片段（复制粘贴即用）

csharp



```天数
// Day1：现代C#写法（一行顶C++十行）
var list = new List<int> {1,2,3,4,5};
var evens = list.Where(x => x % 2 == 0).ToList();               // LINQ
string? name = null;
var len = name?.Length ?? 0;                                   // null安全
var point = new Point(3, 4) with { X = 10 };                    // with表达式
record Point(int X, int Y);                                     // 不可变记录

// Day3：异步取消+进度汇报
var cts = new CancellationTokenSource();
var progress = new Progress<int>(p => Console.WriteLine($"{p}%"));
await Parallel.ForEachAsync(urls, cts.Token, async (url, token) =>
{
    var bytes = await client.GetByteArrayAsync(url, token);
    progress.Report(Interlocked.Increment(ref count) * 100 / urls.Count);
    return bytes;
});

// Day5：Primary Constructor（.NET 8）
public class Service(ILogger<Service> Logger, IConfiguration Config)(string name)
{
    public void Log() => Logger.LogInformation("Hello {Name}", name);
}

// Day9：Span极致性能
public static string ParseCsv(ReadOnlySpan<char> line)
{
    var span = line.Span;
    int index = span.IndexOf(',');
    return span.Slice(0, index).ToString();
}
```