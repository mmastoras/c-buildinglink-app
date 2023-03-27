ARG DOTNET_VERSION_TAG=3.1-alpine3.15

FROM ghcr.io/buildinglink/dotnet-sdk:$DOTNET_VERSION_TAG AS build

ARG GITHUB_TOKEN
RUN dotnet nuget add source https://nuget.pkg.github.com/buildinglink/index.json --name github.com --username github --password $GITHUB_TOKEN --store-password-in-clear-text

WORKDIR /src

#--- building application ---------------------
COPY src/webapp-netcore3.1 ./

RUN dotnet build -c Release

#--- publishing application -------------------
FROM build AS publishApi
RUN dotnet publish --no-build -c Release -o /app/publish

#--- final setup ------------------------------
FROM ghcr.io/buildinglink/dotnet-aspnet:$DOTNET_VERSION_TAG AS final

COPY --from=publishApi /app/publish /helloworld/

WORKDIR /helloworld/

ENTRYPOINT ["dotnet"]
CMD ["HelloWorld.dll"]