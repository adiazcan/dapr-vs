#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["MicroTest.Red.Api/MicroTest.Red.Api.csproj", "MicroTest.Red.Api/"]
RUN dotnet restore "MicroTest.Red.Api/MicroTest.Red.Api.csproj"
COPY . .
WORKDIR "/src/MicroTest.Red.Api"
RUN dotnet build "MicroTest.Red.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MicroTest.Red.Api.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MicroTest.Red.Api.dll"]