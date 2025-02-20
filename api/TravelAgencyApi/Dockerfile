# Usar a imagem base do .NET 8
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 5000
EXPOSE 5001

# SDK para compilar o projeto
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["TravelAgencyApi/TravelAgencyApi.csproj", "TravelAgencyApi/"]
RUN dotnet restore "TravelAgencyApi/TravelAgencyApi.csproj"

# Copia todo o código e compila
COPY . .
WORKDIR "/src/TravelAgencyApi"
RUN dotnet build -c Release -o /app/build

# Publica o projeto
FROM build AS publish
RUN dotnet publish -c Release -o /app/publish

# Configuração do runtime
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "TravelAgencyApi.dll"]
