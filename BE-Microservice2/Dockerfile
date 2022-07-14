#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["BE-Microservice2/BE-Microservice2.csproj", "BE-Microservice2/"]
RUN dotnet restore "BE-Microservice2/BE-Microservice2.csproj"
COPY . .
WORKDIR "/src/BE-Microservice2"
RUN dotnet build "BE-Microservice2.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BE-Microservice2.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BE-Microservice2.dll"]