FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Lading-PagesVer1/Lading-PagesVer1.csproj", "Lading-PagesVer1/"]
RUN dotnet restore "Lading-PagesVer1/Lading-PagesVer1.csproj"
COPY . .
WORKDIR "/src/Lading-PagesVer1"
RUN dotnet build "Lading-PagesVer1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Lading-PagesVer1.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Lading-PagesVer1.dll"]
