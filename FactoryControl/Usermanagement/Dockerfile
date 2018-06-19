FROM microsoft/aspnetcore:2.0-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 58698
EXPOSE 44369

FROM microsoft/aspnetcore-build:2.0-nanoserver-1709 AS build
WORKDIR /src
COPY Usermanagement/Usermanagement.csproj Usermanagement/
RUN dotnet restore Usermanagement/Usermanagement.csproj
COPY . .
WORKDIR /src/Usermanagement
RUN dotnet build Usermanagement.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish Usermanagement.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Usermanagement.dll"]
