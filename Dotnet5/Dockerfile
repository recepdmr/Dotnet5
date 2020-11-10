#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
WORKDIR /src
COPY ["Dotnet5/Dotnet5.csproj", "Dotnet5/"]
RUN dotnet restore "Dotnet5/Dotnet5.csproj"
COPY . .
WORKDIR "/src/Dotnet5"
RUN dotnet build "Dotnet5.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Dotnet5.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Dotnet5.dll"]