FROM mcr.microsoft.com/dotnet/aspnet:4.8 as base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:4.8 as build
WORKDIR /src

COPY MVC_CURD_LIST/MVC_CRUD_LIST.csproj .
RUN dotnet restore MVC_CRUD_LIST/MVC_CRUD_LIST.csproj

COPY . .
RUN dotnet build MVC_CRUD_LIST/MVC_CRUD_LIST.csproj -o ./build

FROM build as publish
RUN dotnet publish MVC_CRUD_LIST/MVC_CRUD_LIST.csproj -c Release -o ./publish /p:UseAppHost=false

FROM base as final
ENV ASPNETCORE_URLS=http://*:8081
COPY --from=publish /src/publish .
ENTRYPOINT ["dotnet", "MVC_CRUD_LIST.dll"]