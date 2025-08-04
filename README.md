# MapGen Service

A .NET 9.0 ASP.NET Core web service for generating procedural maps.

## Features

- REST API for map generation
- Support for different map generation algorithms
- Configurable map parameters (width, height, seed)
- Swagger/OpenAPI documentation
- Dependency injection with Scrutor for assembly scanning

## Project Structure

```
MapGen.Service/
├── Controllers/          # API controllers
├── Services/            # Business logic services
├── Models/              # Data models (if needed)
├── Program.cs           # Application entry point
└── appsettings.json    # Configuration
```

## Getting Started

### Prerequisites

- .NET 9.0 SDK
- Your preferred IDE (Visual Studio, VS Code, Rider, etc.)

### Running the Service

1. Navigate to the project directory:

   ```bash
   cd MapGen.Service
   ```

2. Run the service:

   ```bash
   dotnet run
   ```

3. The service will be available at:
   - API: https://localhost:7001 (or http://localhost:5001)
   - Swagger UI: https://localhost:7001/swagger

## API Endpoints

### Generate Map

- **POST** `/api/map/generate`
- Generates a map with random seed

### Generate Map with Seed

- **POST** `/api/map/generate/{seed}`
- Generates a map with specified seed

### Health Check

- **GET** `/api/map/health`
- Returns service health status

## Example Usage

### Generate a map with default parameters:

```bash
curl -X POST "https://localhost:7001/api/map/generate" \
     -H "Content-Type: application/json" \
     -d '{
       "width": 256,
       "height": 256,
       "algorithm": "perlin",
       "parameters": {
         "scale": 0.1,
         "octaves": 4
       }
     }'
```

### Generate a map with specific seed:

```bash
curl -X POST "https://localhost:7001/api/map/generate/12345" \
     -H "Content-Type: application/json" \
     -d '{
       "width": 512,
       "height": 512,
       "algorithm": "cellular"
     }'
```

## Configuration

The service uses standard ASP.NET Core configuration. Key settings can be modified in `appsettings.json` and `appsettings.Development.json`.

## Development

### Adding New Map Generation Algorithms

1. Create a new service implementing `IMapGenerationService`
2. Register it in `Program.cs` using Scrutor's assembly scanning
3. The service will be automatically available through dependency injection

### Integration with mapgen-core

To integrate with your `mapgen-core` library:

1. Add a project reference to your mapgen-core project:

   ```bash
   dotnet add MapGen.Service reference ../path/to/mapgen-core/MapGen.Core.csproj
   ```

2. Update the `MapGenerationService` to use your core library's functionality

## Dependencies

- **Scrutor**: For assembly scanning and dependency injection
- **Swashbuckle.AspNetCore**: For Swagger/OpenAPI documentation

## License

[Add your license information here]
