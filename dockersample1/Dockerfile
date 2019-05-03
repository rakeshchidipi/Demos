FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["dockersample1/dockersample1.csproj", "dockersample1/"]
RUN dotnet restore "dockersample1/dockersample1.csproj"
COPY . .
WORKDIR "/src/dockersample1"
RUN dotnet build "dockersample1.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "dockersample1.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "dockersample1.dll"]