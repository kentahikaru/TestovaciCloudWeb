FROM mcr.microsoft.com/dotnet/core/aspnet:3.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.0 AS build
WORKDIR /src
COPY ["TestovaciCloudWeb/TestovaciCloudWeb.csproj", "TestovaciCloudWeb/"]

RUN dotnet restore "TestovaciCloudWeb/TestovaciCloudWeb.csproj"
COPY . .
WORKDIR "/src/TestovaciCloudWeb"
RUN dotnet build "TestovaciCloudWeb.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "TestovaciCloudWeb.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "TestovaciCloudWeb.dll"]