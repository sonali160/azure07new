#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["azure07new/azure07new.csproj", "azure07new/"]
RUN dotnet restore "azure07new/azure07new.csproj"
COPY . .
WORKDIR "/src/azure07new"
RUN dotnet build "azure07new.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "azure07new.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "azure07new.dll"]