FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 53478
EXPOSE 44396

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY TestNetCoreDocker/TestNetCoreDocker.csproj TestNetCoreDocker/
RUN dotnet restore TestNetCoreDocker/TestNetCoreDocker.csproj
#RUN ["dotnet", "restore","TestNetCoreDocker/TestNetCoreDocker.csproj"]
 
COPY . .
WORKDIR /src/TestNetCoreDocker
RUN dotnet build TestNetCoreDocker.csproj -c Release -o /app
#RUN ["dotnet", "build","TestNetCoreDocker.csproj -c Release -o /app"]

FROM build AS publish
RUN dotnet publish TestNetCoreDocker.csproj -c Release -o /app
#RUN ["dotnet", "publish","TestNetCoreDocker.csproj -c Release -o /app"]

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "testnetcoredocker.dll"]
