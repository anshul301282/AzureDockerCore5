#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["DockerCore5.csproj", "."]
RUN dotnet restore "./DockerCore5.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "DockerCore5.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DockerCore5.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DockerCore5.dll"]