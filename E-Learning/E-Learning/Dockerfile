FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["E-Learning/E-Learning.csproj", "E-Learning/"]
RUN dotnet restore "E-Learning/E-Learning.csproj"
COPY . .
WORKDIR "/src/E-Learning"
RUN dotnet build "E-Learning.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "E-Learning.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "E-Learning.dll"]
