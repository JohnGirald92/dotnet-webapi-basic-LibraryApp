FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443


# Usar la imagen SDK para compilar el proyecto
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["./", "LibraryApp.WebApi/"]
RUN dotnet restore "LibraryApp.WebApi/LibraryApp.WebApi.csproj"
COPY . .
WORKDIR "/src/LibraryApp.WebApi"
RUN dotnet build "LibraryApp.WebApi.csproj" -c Release -o /app/build


FROM build AS publish
RUN dotnet publish "LibraryApp.WebApi.csproj" -c Release -o /app/publish /p:UseAppHost=false


FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "LibraryApp.WebApi.dll"]
