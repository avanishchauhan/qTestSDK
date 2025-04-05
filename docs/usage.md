# 🚀 Usage

This guide shows how to set up and consume the SDK in a .NET application using Dependency Injection and Serilog logging.

## 🧱 Program.cs Example

```csharp
var config = new ConfigurationBuilder()
    .AddJsonFile("appsettings.json")
    .AddJsonFile($"appsettings.{Environment.GetEnvironmentVariable("DOTNET_ENVIRONMENT")}.json", optional: true)
    .Build();

Log.Logger = new LoggerConfiguration()
    .ReadFrom.Configuration(config)
    .CreateLogger();

var services = new ServiceCollection();
services.AddLogging(logging =>
{
    logging.ClearProviders();
    logging.AddSerilog();
});

var sdkOptions = config.GetSection("qTest").Get<QTestSdkOptions>() ?? new();

services.AddQTestSdk(options =>
{
    options.BaseUrl = sdkOptions.BaseUrl;
    options.AuthToken = sdkOptions.AuthToken;
    options.RateLimiter = sdkOptions.RateLimiter;
    options.RetryPolicy = sdkOptions.RetryPolicy;
    options.CircuitBreaker = sdkOptions.CircuitBreaker;
});

var provider = services.BuildServiceProvider();
var client = provider.GetRequiredService<IProjectClient>();

var projects = await client.GetAllAsync();
Console.WriteLine($"Retrieved {projects.Count()} projects.");
