# 📝 Logging

Logging is handled through `ILogger<T>` interfaces, keeping the SDK agnostic of any logging framework.

## 🎯 Logging Highlights

- No Serilog/NLog dependency in SDK
- Structured and human-readable logs supported
- Log levels and sinks are controlled by the host application

## ✅ Sample Log Messages

```csharp
_logger.LogInformation("Fetching all qTest projects...");
_logger.LogInformation("Retrieved {Count} project(s)", projects.Count());
