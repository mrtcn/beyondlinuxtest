FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY DockerLinuxTest/DockerLinuxTest.csproj DockerLinuxTest/
RUN dotnet restore DockerLinuxTest/DockerLinuxTest.csproj
COPY . .
WORKDIR /src/DockerLinuxTest
RUN dotnet build DockerLinuxTest.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish DockerLinuxTest.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DockerLinuxTest.dll"]
