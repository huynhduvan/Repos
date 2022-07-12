FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Lading-Pages/Lading-Pages.csproj", "Lading-Pages/"]
RUN dotnet restore "Lading-Pages/Lading-Pages.csproj"
COPY . .
WORKDIR "/src/Lading-Pages"
RUN dotnet build "Lading-Pages.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Lading-Pages.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Lading-Pages.dll"]
