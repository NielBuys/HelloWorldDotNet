# Stage 1: Build with SDK
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build

WORKDIR /app

# Copy project files and restore dependencies
COPY ../*.csproj ./
RUN dotnet restore

# Copy everything else and publish
COPY ../. ./

RUN dotnet publish -c Release -o out

# Stage 2: Runtime image
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS runtime
WORKDIR /app

# Copy published output from build stage
COPY --from=build /app/out ./

# Expose port if your app listens on one (optional)
EXPOSE 5000

# Start the app
ENTRYPOINT ["dotnet", "HWDotNet.dll"]
