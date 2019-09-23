FROM mcr.microsoft.com/dotnet/core/sdk:3.0.100-preview8-disco as build
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - && apt-get install -y nodejs
WORKDIR /web
COPY src/ /web
RUN dotnet publish -c Release

FROM mcr.microsoft.com/dotnet/core/aspnet:3.0.0-preview8-disco
WORKDIR /web
COPY --from=build /web/bin/Release/netcoreapp3.0/publish /web
ENTRYPOINT ["dotnet", "/web/app.dll"]
