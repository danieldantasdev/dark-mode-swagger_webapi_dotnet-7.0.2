FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["DarkMode.Swagger.Api/DarkMode.Swagger.Api.csproj", "DarkMode.Swagger.Api/"]
RUN dotnet restore "DarkMode.Swagger.Api/DarkMode.Swagger.Api.csproj"
COPY . .
WORKDIR "/src/DarkMode.Swagger.Api"
RUN dotnet build "DarkMode.Swagger.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DarkMode.Swagger.Api.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DarkMode.Swagger.Api.dll"]
