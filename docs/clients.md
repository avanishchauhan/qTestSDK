# 🧩 SDK Clients

The SDK provides typed API clients with built-in retry, rate limiting, and logging support.

## ✅ Available Clients

| Interface         | Implementation     | Purpose                 |
|------------------|---------------------|--------------------------|
| `IProjectClient` | `ProjectClient`     | Access qTest projects    |
| `ITestCaseClient`| _(Planned)_         | Manage test cases        |
| `ITestRunClient` | _(Planned)_         | Manage test executions   |

## ➕ Registering Clients

All clients are registered using:

```csharp
services.AddQTestClient<IProjectClient, ProjectClient>(options);
