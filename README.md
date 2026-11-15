# 学习 Kotlin 2.4

📖 **阅读教程：[https://stahe.github.io/zh-kotlin-oct-2026/](https://stahe.github.io/zh-kotlin-oct-2026/)**

本课程**通过示例**教你 [Kotlin](https://kotlinlang.org/) 2.4 语言：两百多个程序（337 个 Kotlin 文件），逐行注释，并附有其运行结果。课程从语言基础开始，涵盖协程、使用 JDBC 和 Hibernate 访问数据库、网络编程，以及使用 Spring Boot 的 Web 服务。

这是课程[学习 Java 25 语言](https://stahe.github.io/zh-java-oct-2026/)（2026 年 10 月）的 Kotlin 版本，而该课程本身又是 [C# 14](https://stahe.github.io/zh-csharp-oct-2026/) 课程的移植——后者是对 2008 年一门 C# 课程的重写：大纲相同、示例相同、贯穿全程的主题相同，只是用当今的 Kotlin 编写。所有程序都使用 Kotlin 2.4.20（警告视为错误）**无错误、无警告**地编译，并在 JDK 25 上运行；课程中重现的结果均来自这些运行。

| Java 25 课程（2026） | Kotlin 2.4 课程（2026） |
|---|---|
| Java 25（LTS）、JDK 25 | Kotlin 2.4.20、JDK 25 |
| 紧凑源文件（`java Prog.java`） | 高层 `main` 函数、`kotlinc`、IntelliJ IDEA 绿色三角形 |
| Maven 项目（`pom.xml`） | 使用 Kotlin DSL 的 Gradle 项目（`build.gradle.kts`）、Gradle 9.8 wrapper |
| `null`、包装类和 `Optional` | 类型系统中的 `null` 安全（`?.`、`?:`、`!!`） |
| 访问器、记录、无运算符重载 | 属性、数据类、运算符重载、扩展函数 |
| 受检异常、带资源的 `try` | 全部为非受检异常、`use` |
| Stream API | 集合操作、序列 |
| 函数式接口、lambda | 函数类型、lambda、`inline` 函数、委托属性 |
| `CompletableFuture`、虚拟线程 | **协程**：`suspend`、`launch` / `async`、结构化并发、`Flow`、`Channel` |
| JUnit 6、Spring Framework 7 | JUnit 6 和 `kotlin.test`、Spring Framework 7（`kotlin-spring` 插件） |
| Jackson 3 | 搭配数据类的 Jackson 3 |
| JDBC、MySQL Connector/J、HikariCP | 相同，使用 Kotlin 惯用法 |
| Hibernate 7 | 搭配 `kotlin-jpa`（无参）和 all-open 插件的 Hibernate 7 |
| `HttpClient`、`Socket` / `ServerSocket` | 相同的类，用 Kotlin 编写 |
| Spring Boot 4 | Kotlin 中的 Spring Boot 4 |

## 课程大纲

| 章节 | 内容 |
|---|---|
| 安装 | JDK 25、IntelliJ IDEA / VS Code、`kotlinc` 编译器、Gradle（wrapper、Kotlin DSL）、多模块项目 |
| 语言基础 | 类型、`val` / `var`、类型推断、字符串模板、原始字符串、`null` 安全、转换、数组、运算符、`when`、区间和循环、异常、`use`、枚举、默认参数和具名参数、局部函数、`Pair` 和解构 |
| 类、接口、数据类 | 主构造函数、属性、`object` 和 `companion object`、继承、密封类、运算符重载、索引器、值类、扩展函数、接口、抽象类、泛型和型变、包、数据类、智能类型转换 |
| 常用的 Kotlin 类 | 字符串、数组、只读集合和可变集合、函数式操作、**序列**、文本和二进制文件、使用 Jackson 3 处理 JSON、正则表达式（`Regex`） |
| 分层架构 | [DAO] / [业务逻辑] / [UI]、多项目 Gradle 构建、**JUnit 6** 和 `kotlin.test` 单元测试、使用 Spring 的**依赖注入** |
| 函数类型、lambda 和事件 | 函数类型、lambda、函数引用、`fun interface`、闭包、组合、`inline` 函数、监听器、可观察的委托属性 |
| 执行线程 | `thread { }`、**虚拟线程**、`synchronized`、`@Volatile`、`ReentrantLock`、`Condition`、原子操作、信号量、并发集合、`ExecutorService`、fork/join、`ThreadLocal`、`ScopedValue` |
| 异步编程 | **协程**：`suspend` 函数、`runBlocking`、`launch`、`async` / `await`、调度器、结构化并发、异常、取消和超时、`Flow`、`Channel`、`CompletableDeferred`、受限并行度、协程与虚拟线程 |
| 使用 JDBC 访问数据库 | MySQL、MySQL Connector/J、`DataSource` 和 HikariCP、参数化查询和 SQL 注入、事务、批处理、结合虚拟线程和协程的 JDBC |
| **Hibernate** | Kotlin 实体、`SessionFactory` / `Session`、CRUD、HQL 和 Criteria API、关系、迁移、乐观并发、原生 SQL、Spring ORM 和 `@Transactional` |
| Web 编程 | TCP/IP、IPv6、TCP 客户端和服务器（每个客户端一个虚拟线程）、HTTP、`HttpClient`、使用 Jakarta Mail 的 SMTP |
| Web 服务 | 使用 Kotlin 中 **Spring Boot 4** 的 REST / JSON、Kotlin 控制台客户端、JavaScript Web 客户端、Node.js 客户端 |

## 贯穿主线：9 个版本的税款计算器

在整个课程中，我们逐个版本地构建一个**计算所得税**的应用：

- **版本 1**：单个程序；**版本 2**：类和接口；**版本 3**：从文本文件或 JSON 文件读取数据；
- **版本 4 和 5**：分层架构，组织为 Gradle 子项目，用 JUnit 测试，并通过 Spring 依赖注入集成；
- **版本 6 和 7**：数据存储在 MySQL 数据库中，先用 JDBC 再用 Hibernate 检索；
- **版本 8**：税款计算的 TCP 服务器及其客户端；
- **版本 9**：Spring Boot REST Web 服务、其控制台客户端及其 Web 客户端。

## 技术

Kotlin 2.4.20 · JDK 25 · Gradle 9.8（Kotlin DSL）· IntelliJ IDEA · kotlinx.coroutines 1.11 · JUnit 6 · Spring Framework 7 · Jackson 3 · MySQL 8 · MySQL Connector/J 9 · HikariCP · Hibernate ORM 7.4 · Jakarta Persistence 3.2 · Spring Boot 4.1 · Laragon

## 先决条件

- 具备任意一种语言的编程经验。
- [JDK 25](https://adoptium.net)（Eclipse Temurin 或其他发行版）和 [IntelliJ IDEA](https://www.jetbrains.com/idea/)（内置 Kotlin）。无需安装 Gradle：每个章节文件夹都包含自己的 wrapper（`gradlew`）。如果未安装 JDK 25，Gradle 会自动下载（使用 `foojay-resolver-convention` 插件）。数据库章节需要用 [Laragon](https://laragon.org) 提供 MySQL。课程中提供了安装说明。

## 作者

本课程及其代码由 [Anthropic](https://www.anthropic.com) 的 AI **Claude** 编写（2026 年 10 月），应 Serge Tahé 的请求完成，基于他的 Java 25 课程。

审阅：[Serge Tahé](https://stahe.github.io)
