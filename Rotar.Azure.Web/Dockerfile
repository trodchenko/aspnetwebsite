FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["Rotar.Azure.Web/Rotar.Azure.Web.csproj", "Rotar.Azure.Web/"]
RUN dotnet restore "Rotar.Azure.Web/Rotar.Azure.Web.csproj"
COPY . .
WORKDIR "/src/Rotar.Azure.Web"
RUN dotnet build "Rotar.Azure.Web.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Rotar.Azure.Web.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Rotar.Azure.Web.dll"]