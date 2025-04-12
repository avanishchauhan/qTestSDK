# qTest .NET SDK

A resilient, configurable .NET SDK for interacting with the [qTest API](https://www.tricentis.com/products/qtest). Built with extensibility, retry handling, and rate limiting for enterprise-grade scenarios.

---

## ✨ Features

- Typed clients for qTest modules (Projects, Test Cases, Test Runs, etc.)
- Configurable rate limiting via `System.Threading.RateLimiting`
- Automatic retries with Polly-based exponential/backoff strategies
- Circuit breaker support
- Token-based authentication with automatic rotation
- Clean dependency injection support with `HttpClientFactory`
- Structured logging using `ILogger<T>`

---

## 📦 Installation

Add a reference to your project via NuGet:

```bash
Install-Package qTest.SDK
```

---

## ⚙️ Configuration

Your `appsettings.json` should look like:

```json
"qTest": {
  "BaseUrl": "https://your-domain.qtestnet.com/api/v3/",
  "Username": "your-username",
  "Password": "your-password",
  "SiteName": "your-domain",

  "RateLimiter": {
    "TokenLimit": 60,
    "TokensPerPeriod": 60,
    "ReplenishmentPeriod": "00:01:00"
  },

  "ApiSettings": {
    "RetryPolicy": {
      "RetryCount": 3,
      "BaseDelay": "00:00:01",
      "DecayType": "Exponential"
    },
    "CircuitBreaker": {
      "FailuresBeforeBreak": 5,
      "DurationOfBreak": "00:00:30"
    }
  },

  "AuthSettings": {
    "RetryPolicy": {
      "RetryCount": 2,
      "BaseDelay": "00:00:01",
      "DecayType": "Exponential"
    },
    "CircuitBreaker": {
      "FailuresBeforeBreak": 3,
      "DurationOfBreak": "00:00:20"
    }
  }
}
```

---

## 🧪 Sample Usage

```csharp
var config = configuration.GetSection("qTest").Get<QTestSdkOptions>();

services.AddQTestSdk(options =>
{
    options.BaseUrl = config.BaseUrl;
    options.Username = config.Username;
    options.Password = config.Password;
    options.SiteName = config.SiteName;
    options.RateLimiter = config.RateLimiter;
    options.ApiSettings = config.ApiSettings;
    options.AuthSettings = config.AuthSettings;
});

var projectClient = provider.GetRequiredService<IProjectClient>();
var projects = await projectClient.GetAllAsync();
```

---

## 🔐 Authentication

- The SDK automatically fetches a bearer token using the `username`, `password`, and `SiteName`
- Tokens are cached and auto-refreshed via `CachedLoginTokenProvider`
- Uses `Authorization: Basic base64(SiteName:)` with form-encoded body

---

## 🔁 Resilience Strategy

- **Rate limiting** with configurable token buckets
- **Retries** with exponential or linear backoff using Polly
- **Circuit breakers** to avoid hammering unstable services
- **Delegating handlers** wrap each client with resilience logic via `ResilienceHandler<T>`

---

## 📋 Logging

- Uses `ILogger<T>` throughout
- Log output can be routed via Serilog or any other provider
- All major events (token usage, request sending, retry attempts) are logged

---

## 🧪 Testing

- Core components have isolated unit tests with Moq and xUnit
- Auth and token flows fully tested

---

## 🔧 Extensibility

- Plug in your own `GetTokenAsync` implementation
- Override resilience settings per client
- Add new clients by extending `IProjectClient`-style pattern

---

## 📄 License

This SDK is not open source. It is licensed for internal or customer-specific use only.
