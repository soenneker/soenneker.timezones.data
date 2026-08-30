[![](https://img.shields.io/nuget/v/soenneker.timezones.data.svg?style=for-the-badge)](https://www.nuget.org/packages/soenneker.timezones.data/)
[![](https://img.shields.io/github/actions/workflow/status/soenneker/soenneker.timezones.data/build-and-test.yml?style=for-the-badge)](https://github.com/soenneker/soenneker.timezones.data/actions/workflows/build-and-test.yml)
[![](https://img.shields.io/nuget/dt/soenneker.timezones.data.svg?style=for-the-badge)](https://www.nuget.org/packages/soenneker.timezones.data/)
[![](https://img.shields.io/github/actions/workflow/status/soenneker/soenneker.timezones.data/codeql.yml?style=for-the-badge)](https://github.com/soenneker/soenneker.timezones.data/actions/workflows/codeql.yml)

# Soenneker.TimeZones.Data

Packages generated geographic boundaries for IANA time zones as GeoJSON content.

## Installation

```bash
dotnet add package Soenneker.TimeZones.Data
```

The package copies `Resources/timezones.geojson` into the consuming application's output. It contains a GeoJSON `FeatureCollection`; each usable feature identifies a zone through `properties.tzid` and supplies polygon or multipolygon geometry.

```csharp
string path = Path.Combine(
    AppContext.BaseDirectory,
    "Resources",
    "timezones.geojson");

await using FileStream stream = File.OpenRead(path);
using JsonDocument document = await JsonDocument.ParseAsync(stream);
```

This package contains data, not a lookup API. For coordinate-to-zone resolution, use `Soenneker.TimeZones.Lookup`, which loads this resource and handles polygon containment.

Time-zone boundaries change. Pin a package version when reproducible geographic results matter, and update deliberately after validating coordinates important to the application.
