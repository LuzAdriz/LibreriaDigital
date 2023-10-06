FROM mcr.microsoft.com/dotnet/aspnet:7.0 As base
WORKDIR /app
EXPOSE 80
EXPOSE 443

# Usar la imagen SDK para compilar el proyecto
FROM mcr.microsoft.com/dotnet/sdk:7.0 As build
WORKDIR /src
COPY ["./", "LibreriaDigital.WebApi/"]
RUN dotnet restore "LibreriaDigital.WebApi.csproj"
COPY . .
WORKDIR "/src/LibreriaDigital.WebApi"
RUN dotnet build "LibreriaDigital.WebApi.csproj" -c Release -o /app/build

FROM build As publish
RUN dotnet publish "LibreriaDigital.WebApi.csproj" -c Release -o /app/publish /p:UseAppHost-false

FROM base As final
WORKDIR /app
COPY from-publish /app/publish 
ENTRYPOINT ["dotnet", "LibreriaDigital.WebApi.dll"]
