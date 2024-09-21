# Features

`ChrisMavrommatis.Features` is a .NET library that provides a flexible and extensible solution for managing features in a software application. It allows you to enable or disable specific features based on various conditions, such as configuration settings or environment variables.

## Installation

Install the package via NuGet Package Manager
```bash
Install-Package ChrisMavrommatis.Features
```

Or via .NET CLI:
```bash
dotnet add package ChrisMavrommatis.Features
```

## Usage

In your startup class configure the static `Feature.Manager` instance using the following code:

```csharp
Feature.Manager = new FeatureManagerConfiguration()
			.ReadFrom.EnvironmentVariables()
			.ReadFrom.Configuration(builder.Configuration)
			.CreateManager();

```

Be sure to have loaded the configuration from a file or other source beforehand
```csharp
builder.Configuration
	.AddJsonFile("Features.json", optional: false, reloadOnChange: true)
	.AddJsonFile($"Features.{builder.Environment.EnvironmentName}.json", optional: true, reloadOnChange: true);
```

The json should look like this

```json
{
  "Features": {
    "Feature1": true
    "Feature2": false
  }
}
```

Then you  can call the method `IsEnabled` on the static `Feature`
```csharp
if (Feature.IsEnabled("Feature1"))
{
	// Do something
}
```

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

