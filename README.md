# .NET 10 isolated Azure Functions sample

This is a .NET 10 isolated worker app for Azure Functions v4. It exposes
`Function1` over HTTP GET and POST with function-level authorization.

## Build

Install a .NET 10 SDK, then run the same command used by the GitHub Actions
workflows from the repository root:

```sh
dotnet build --configuration Release --output ./output
```

The `global.json` selects the latest installed .NET 10.0.1xx SDK patch. For local
execution, install Azure Functions Core Tools v4 and create an untracked
`local.settings.json` with `FUNCTIONS_WORKER_RUNTIME` set to `dotnet-isolated`
and a suitable `AzureWebJobsStorage` connection; then run `func start`.

## Deployment workflows

The four existing workflows build this project with .NET 10. Their deployment
steps (including Azure login) are disabled until the repository variable
`DOTNET10_DEPLOY_READY` is set to `true`. Before opting in, verify **each**
named destination app supports .NET 10 isolated on Functions v4 and is
configured to run it (`FUNCTIONS_WORKER_RUNTIME=dotnet-isolated`). In
particular, .NET 10 is **not supported on Linux Consumption**; migrate such
apps to a supported plan such as Flex Consumption before deploying. The
workflows retain their original app names, credentials, and deployment slots.

See the [Azure Functions isolated worker guide](https://learn.microsoft.com/azure/azure-functions/dotnet-isolated-process-guide)
for hosting and runtime configuration details.
