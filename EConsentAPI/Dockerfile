FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["EConsentAPI/EConsentAPI.csproj", "EConsentAPI/"]
RUN dotnet restore "EConsentAPI/EConsentAPI.csproj"
COPY . .
WORKDIR "/src/EConsentAPI"
RUN dotnet build "EConsentAPI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "EConsentAPI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "EConsentAPI.dll"]