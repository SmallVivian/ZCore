FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["ZCore.Salor/ZCore.Salor.csproj", "ZCore.Salor/"]
RUN dotnet restore "ZCore.Salor/ZCore.Salor.csproj"
COPY . .
WORKDIR "/src/ZCore.Salor"
RUN dotnet build "ZCore.Salor.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "ZCore.Salor.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ZCore.Salor.dll"]