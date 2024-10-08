# 哨兵调试日志

## 日志记录总则

1. 日志中不要记录无用信息，防止无用日志淹没重要信息
2. 要明确不同日志的用途，对日志内容进行分类
3. 日志信息要准确全面，努力做到仅凭日志就可以定位问题
4. 日志格式要统一规范
5. 日志要不断优化、完善

## 日志级别

遵循 [RFC 5424](https://link.zhihu.com/?target=https%3A//tools.ietf.org/html/rfc5424)，将日志级别分为以下 8 种等级：

- 0 Emergency: system is unusable
- 1 Alert: action must be taken immediately
- 2 Critical: critical conditions
- 3 Error: error conditions
- 4 Warning: warning conditions
- 5 Notice: normal but significant condition
- 6 Informational: informational messages
- 7 Debug: debug-level messages

各级日志等级信息记录内容如下：

### Emergency

- 导致系统不可用的事故，属于最严重的日志级别，因此该日志级别必须慎用
- 通常情况下，**一个进程的声明周期中应该只记录一次 Emergency 级别的日志**

### Alert

- 必须马上处理的问题，紧急程度低于 Emergency
- Alert 错误发生时，已经影响了用户的正常访问
- 与 Emergency 的区别是，Alert 状态下系统依旧是可用的。例如：DB / Cache 无法连接。

### Critical

紧急情况，程序组件不可用，需要立刻进行修复。例如：用户注册逻辑模块不能发送邮件。

### Error

- 运行时出现的错误，不必要立即进行修复
- 错误不影响整个逻辑的运行，但需要记录并做检测。

### Warning

- 可能影响系统功能，需要提醒的重要事件
- 该日志标示系统可能出现问题，也可能没有（比如网络波动）。对于那些目前还不是错误，然而不及时处理也会变为错误的情况，也可以记为 Warning 日志。例如一个存储系统的磁盘使用量超过阀值，或者系统中某个用户的存储配额快用完等等
- 对于 Warining 级别的日志，虽然不需要马上处理，但也需要及时查看并处理

### Notice

- 不影响正常功能，但需要注意的消息
- 执行过程中较 Infomational 级别更为重要的信息。

### Infomational

- 用于记录系统正常运行情况下的一般信息，强调应用程序的运行过程。例如：某个子模块的初始化、某个请求的成功执行等
- 通过查看 Infomational 级别的日志，可以很快对系统中出现的 0~5 级别的错误进行定位

### Debug

帮助开发、测试、运维人员对系统进行诊断的信息。
