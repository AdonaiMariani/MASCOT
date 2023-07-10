FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /app

# Copio los archivos
COPY . .

# restauro paquetes
RUN dotnet restore

# compilo
RUN dotnet build --no-restore --configuration Release

# publico
RUN dotnet publish --no-restore --configuration Release --output /app/publish

# creación de imagen final
FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app
COPY --from=build /app/publish .

# connect db
# Configuración de la base de datos
ENV ConnectionStrings__Conexion="Server=.\\SQLExpress;Database=Veterinaria;Trusted_Connection=True;"

# Configuración de Swagger
ENV ASPNETCORE_ENVIRONMENT="Development"
ENV ASPNETCORE_URLS="http://+:7045"
EXPOSE 7045


# ejecutar app
ENTRYPOINT ["dotnet", "BE-CRUDMascotas.dll"]

