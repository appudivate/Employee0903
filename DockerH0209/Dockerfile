#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["DockerH0209/DockerH0209.csproj", "DockerH0209/"]
RUN dotnet restore "DockerH0209/DockerH0209.csproj"
COPY . .
WORKDIR "/src/DockerH0209"
RUN dotnet build "DockerH0209.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DockerH0209.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DockerH0209.dll"]