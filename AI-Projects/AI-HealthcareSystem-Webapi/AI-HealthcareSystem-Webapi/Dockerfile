#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["AI-HealthcareSystem-Webapi/AI-HealthcareSystem-Webapi.csproj", "AI-HealthcareSystem-Webapi/"]
RUN dotnet restore "AI-HealthcareSystem-Webapi/AI-HealthcareSystem-Webapi.csproj"
COPY . .
WORKDIR "/src/AI-HealthcareSystem-Webapi"
RUN dotnet build "AI-HealthcareSystem-Webapi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "AI-HealthcareSystem-Webapi.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AI-HealthcareSystem-Webapi.dll"]