# 🔁 Retry Strategy

This SDK uses [Polly](https://github.com/App-vNext/Polly) to handle transient faults and implements retry and circuit breaker policies.

## ✅ Conditions That Trigger Retry

| Condition                         | Retries? |
|----------------------------------|----------|
| `HttpRequestException` (network) | ✅ Yes   |
| `408 Request Timeout`            | ✅ Yes   |
| `429 Too Many Requests`          | ✅ Yes   |
| `5xx Server Errors`              | ✅ Yes   |
| `400`, `401`, `403`, `404`, etc. | ❌ No    |

Only transient and server errors are retried. Client errors like `401` or `404` are not retried.

## 🔧 Retry Options

These options are defined in `RetryPolicy` inside `appsettings.json`:

```json
"RetryPolicy": {
  "RetryCount": 3,
  "BaseDelay": "00:00:01",
  "DecayType": "Exponential"
}
