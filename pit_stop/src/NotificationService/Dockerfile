FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build-env
WORKDIR /app

# Copy necessary files and restore as distinct layer
COPY Directory.Packages.props ./
RUN dotnet restore

# Copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/sdk:8.0
WORKDIR /app
COPY --from=build-env /app/out .

# Start
ENTRYPOINT ["dotnet", "Pitstop.NotificationService.dll"]
