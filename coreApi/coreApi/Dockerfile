FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["coreApi/coreApi.csproj", "coreApi/"]
RUN dotnet restore "coreApi/coreApi.csproj"
COPY . .
WORKDIR "/src/coreApi"
RUN dotnet build "coreApi.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "coreApi.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "coreApi.dll"]