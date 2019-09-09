FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["GICProductsMicroservice/GICProductsMicroservice.csproj", "GICProductsMicroservice/"]
RUN dotnet restore "GICProductsMicroservice/GICProductsMicroservice.csproj"
COPY . .
WORKDIR "/src/GICProductsMicroservice"
RUN dotnet build "GICProductsMicroservice.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "GICProductsMicroservice.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "GICProductsMicroservice.dll"]