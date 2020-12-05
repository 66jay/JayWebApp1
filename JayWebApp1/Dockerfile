#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["JayWebApp1/JayWebApp1.csproj", "JayWebApp1/"]
RUN dotnet restore "JayWebApp1/JayWebApp1.csproj"
COPY . .
WORKDIR "/src/JayWebApp1"
RUN dotnet build "JayWebApp1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "JayWebApp1.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "JayWebApp1.dll"]