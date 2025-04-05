# 🔧 Configuration

The qTest .NET SDK supports flexible configuration using `appsettings.json` and environment-specific overrides via `DOTNET_ENVIRONMENT`.

## 📁 appsettings.json Structure

```json
{
  "qTest": {
    "BaseUrl": "https://your-qtest-domain/api/v3",
    "AuthToken": "your-api-token",
    "RateLimiter": {
      "MaxRequestsPerMinute": 60
    },
    "RetryPolicy": {
      "RetryCount": 3,
      "BaseDelay": "00:00:01",
      "DecayType": "Exponential"
    },
    "CircuitBreaker": {
      "FailuresBeforeBreak": 5,
      "DurationOfBreak": "00:00:30"
    }
  }
}
