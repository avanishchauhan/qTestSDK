# 🛣 Roadmap

This SDK is under active development. Here’s what’s planned, in progress, or complete.

## ✅ Completed

- [x] Project client with typed interface
- [x] Retry with exponential backoff (via Polly)
- [x] Circuit breaker support
- [x] Token bucket rate limiting
- [x] Logging via `ILogger<T>` abstraction
- [x] Serilog sample with console + JSON logging
- [x] Config-based + programmatic overrides
- [x] Modular documentation in Markdown

## 🛠 In Progress / Planned

- [ ] Add `TestCaseClient`, `TestRunClient`
- [ ] Add pagination & filtering helpers
- [ ] Add hooks for custom headers (user-agent, correlation ID)
- [ ] OpenTelemetry tracing support
- [ ] Publish NuGet package(s)
- [ ] Vault/Secrets Manager sample integration

## 🧪 Testing & Quality

- [ ] Unit tests for clients and config components
- [ ] Integration tests with qTest sandbox
- [ ] Retry + circuit breaker behavior tests
- [ ] Rate limiter under concurrency load

## 📦 Packaging & CI

- [ ] Create `.nuspec` file
- [ ] Add GitHub Actions pipeline
- [ ] Include SourceLink and XML docs
- [ ] Document package dependency guidelines
