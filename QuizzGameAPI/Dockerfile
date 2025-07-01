# Base image
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80

# Build image
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["QuizzGameAPI.csproj", "./"]
RUN dotnet restore "./QuizzGameAPI.csproj"
COPY . .
RUN dotnet build "QuizzGameAPI.csproj" -c Release -o /app/build

# Publish image
FROM build AS publish
RUN dotnet publish "QuizzGameAPI.csproj" -c Release -o /app/publish /p:UseAppHost=false

# Final image
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "QuizzGameAPI.dll"]