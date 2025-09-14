# ASP.NET Blazor Server Application

A modern web application built with ASP.NET Core 9.0 and Blazor Server components.

## 🚀 Quick Start

### Prerequisites

Before you begin, ensure you have the following installed on your Mac:

- **.NET 9.0 SDK** - [Download here](https://dotnet.microsoft.com/download/dotnet/9.0)
- **Git** - Usually pre-installed on macOS, or install via [Homebrew](https://brew.sh/)
- **Visual Studio Code** (recommended) or **Visual Studio for Mac**

### Installation

1. **Clone the repository**
   ```bash
   git clone <your-repository-url>
   cd aspnet
   ```

2. **Verify .NET installation**
   ```bash
   dotnet --version
   # Should show 9.0.x or higher
   ```

3. **Restore dependencies**
   ```bash
   dotnet restore
   ```

4. **Build the project**
   ```bash
   dotnet build
   ```

5. **Run the application**
   ```bash
   dotnet run --project aspnet
   ```

6. **Open in browser**
   - Navigate to `https://localhost:5001` or `http://localhost:5000`
   - The application will automatically open in your default browser

## 🛠️ Development Setup

### Recommended VS Code Extensions

Install these extensions for the best development experience:

```bash
# Install VS Code extensions via command line
code --install-extension ms-dotnettools.csharp
code --install-extension ms-dotnettools.blazorwasm-companion
code --install-extension ms-vscode.vscode-json
code --install-extension bradlc.vscode-tailwindcss  # If using Tailwind CSS
```

Or search for these in VS Code Extensions marketplace:
- **C# Dev Kit** - IntelliSense, debugging, and project management
- **Blazor WASM Companion** - Enhanced Blazor development
- **JSON** - JSON file support
- **Auto Rename Tag** - Automatically rename paired HTML/XML tags

### Project Structure

```
aspnet/
├── Components/           # Blazor components
│   ├── Layout/          # Layout components (MainLayout, NavMenu)
│   ├── Pages/           # Page components (Home, Counter, Weather)
│   ├── App.razor        # Root component
│   ├── Routes.razor     # Routing configuration
│   └── _Imports.razor   # Global using statements
├── Properties/          # Launch settings
├── wwwroot/            # Static files (CSS, JS, images)
├── appsettings.json    # Application configuration
├── Program.cs          # Application entry point
└── aspnet.csproj       # Project file
```

## 🔧 Development Commands

### Building and Running

```bash
# Clean build artifacts
dotnet clean

# Restore NuGet packages
dotnet restore

# Build the project
dotnet build

# Run in development mode (with hot reload)
dotnet run --project aspnet

# Run in watch mode (auto-restart on file changes)
dotnet watch --project aspnet

# Build for production
dotnet build --configuration Release

# Publish for deployment
dotnet publish --configuration Release --output ./publish
```

### Testing

```bash
# Run all tests
dotnet test

# Run tests with coverage
dotnet test --collect:"XPlat Code Coverage"

# Run specific test project
dotnet test path/to/test/project
```

## 🌐 Environment Configuration

### Development Settings

The application uses different configuration files for different environments:

- `appsettings.json` - Base configuration
- `appsettings.Development.json` - Development overrides
- `appsettings.Production.json` - Production overrides (create if needed)

### Environment Variables

Set environment variables for local development:

```bash
# Set development environment
export ASPNETCORE_ENVIRONMENT=Development

# Set custom URLs (optional)
export ASPNETCORE_URLS="https://localhost:5001;http://localhost:5000"

# Add to your ~/.zshrc or ~/.bash_profile for persistence
echo 'export ASPNETCORE_ENVIRONMENT=Development' >> ~/.zshrc
```

## 🐛 Debugging

### VS Code Debugging

1. Open the project in VS Code
2. Go to Run and Debug (⇧⌘D)
3. Select ".NET Core Launch (web)" configuration
4. Set breakpoints in your code
5. Press F5 to start debugging

### Browser Developer Tools

- **Chrome DevTools**: F12 or Cmd+Option+I
- **Blazor debugging**: Enable in browser dev tools under Sources tab

## 📦 Package Management

### Adding NuGet Packages

```bash
# Add a package to the main project
dotnet add aspnet package PackageName

# Add a specific version
dotnet add aspnet package PackageName --version 1.2.3

# Add development-only package
dotnet add aspnet package PackageName --package-directory packages
```

### Updating Packages

```bash
# List outdated packages
dotnet list aspnet package --outdated

# Update all packages
dotnet add aspnet package PackageName

# Update to latest version
dotnet add aspnet package PackageName --version "*"
```

## 🚀 Deployment

### Local Production Build

```bash
# Build for production
dotnet publish aspnet --configuration Release --output ./dist

# Run production build locally
cd dist
dotnet aspnet.dll
```

### Docker (Optional)

Create a `Dockerfile` in the root directory:

```dockerfile
FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src
COPY ["aspnet/aspnet.csproj", "aspnet/"]
RUN dotnet restore "aspnet/aspnet.csproj"
COPY . .
WORKDIR "/src/aspnet"
RUN dotnet build "aspnet.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "aspnet.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "aspnet.dll"]
```

Build and run with Docker:

```bash
# Build Docker image
docker build -t aspnet-app .

# Run container
docker run -p 8080:80 aspnet-app
```

## 🔍 Troubleshooting

### Common Issues

1. **Port already in use**
   ```bash
   # Find process using port 5000/5001
   lsof -ti:5000
   lsof -ti:5001
   
   # Kill process
   kill -9 <PID>
   ```

2. **Certificate issues (HTTPS)**
   ```bash
   # Trust development certificate
   dotnet dev-certs https --trust
   ```

3. **Clear NuGet cache**
   ```bash
   dotnet nuget locals all --clear
   ```

4. **Reset to clean state**
   ```bash
   dotnet clean
   rm -rf bin obj
   dotnet restore
   dotnet build
   ```

### Performance Tips

- Use `dotnet watch` for development to enable hot reload
- Enable browser caching for static assets in production
- Use `--configuration Release` for production builds
- Monitor memory usage with `dotnet-counters`

## 📚 Additional Resources

- [ASP.NET Core Documentation](https://docs.microsoft.com/en-us/aspnet/core/)
- [Blazor Documentation](https://docs.microsoft.com/en-us/aspnet/core/blazor/)
- [.NET CLI Reference](https://docs.microsoft.com/en-us/dotnet/core/tools/)
- [Visual Studio Code for .NET](https://code.visualstudio.com/docs/languages/dotnet)

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
