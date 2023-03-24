ARG DOTNET_VERSION_TAG=6.0-alpine3.15

FROM ghcr.io/buildinglink/dotnet-sdk:$DOTNET_VERSION_TAG AS build

ARG GITHUB_TOKEN
RUN dotnet nuget add source https://nuget.pkg.github.com/buildinglink/index.json --name github.com --username github --password $GITHUB_TOKEN --store-password-in-clear-text

#--- restoring packages -----------------------
WORKDIR /src

COPY src/webapp/HelloWorld.csproj HelloWorld/

RUN dotnet restore HelloWorld/HelloWorld.csproj

#--- building application ---------------------
COPY src/webapp ./

RUN dotnet build HelloWorld/HelloWorld.csproj -c Release

#--- publishing application -------------------
FROM build AS publishApi
RUN dotnet publish HelloWorld/HelloWorld.csproj --no-build -c Release -o /app/publish


#--- final setup ------------------------------
FROM ghcr.io/buildinglink/dotnet-aspnet:$DOTNET_VERSION_TAG AS final

COPY --from=publishApi /app/publish /HelloWorld/

WORKDIR /HelloWorld/

ENTRYPOINT ["dotnet"]
CMD ["HelloWorld.dll"]