FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["AuthAlt/AuthAlt.csproj", "AuthAlt/"]
RUN dotnet restore "AuthAlt/AuthAlt.csproj"
COPY . .
WORKDIR "/src/AuthAlt"
RUN dotnet build "AuthAlt.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "AuthAlt.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AuthAlt.dll"]
