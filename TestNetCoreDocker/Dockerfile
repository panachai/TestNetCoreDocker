FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 53478
EXPOSE 44396


FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY TestNetCoreDocker/TestNetCoreDocker.csproj TestNetCoreDocker/

#RUN dotnet restore TestNetCoreDocker/TestNetCoreDocker.csproj
RUN ["dotnet", "restore"]


COPY . .
WORKDIR /src/TestNetCoreDocker
#RUN dotnet build TestNetCoreDocker.csproj -c Release -o /app
RUN ["dotnet", "build"]


FROM build AS publish
#RUN dotnet publish TestNetCoreDocker.csproj -c Release -o /app
RUN ["dotnet", "publish"]

FROM base AS final
WORKDIR /app

COPY --from=publish /app .
#COPY --from=build-env /app/out ./
#COPY out ./

ENTRYPOINT ["dotnet", "testnetcoredocker.dll"]
