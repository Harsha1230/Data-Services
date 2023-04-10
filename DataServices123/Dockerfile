#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM dataimages123.azurecr.io/runtimesdk:latest AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM dataimages123.azurecr.io/sdk:latest AS build
WORKDIR /src
COPY ["DataServices123/DataServices123/DataServices123.csproj", "DataServices123/"]
RUN dotnet restore "DataServices123/DataServices123.csproj"
COPY DataServices123/. .
WORKDIR "/src/DataServices123"
RUN dotnet build "DataServices123.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DataServices123.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DataServices123.dll"]
