# 📉 Rate Limiting

The SDK uses `System.Threading.RateLimiting` to implement a token-bucket based rate limiter.

## 🔧 Configuration

Define rate limits per minute in `appsettings.json`:

```json
"RateLimiter": {
  "MaxRequestsPerMinute": 60
}
