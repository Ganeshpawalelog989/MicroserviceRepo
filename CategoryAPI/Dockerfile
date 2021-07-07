#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["CategoryAPI/CategoryAPI.csproj", "CategoryAPI/"]
RUN dotnet restore "CategoryAPI/CategoryAPI.csproj"
COPY . .
WORKDIR "/src/CategoryAPI"
RUN dotnet build "CategoryAPI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CategoryAPI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CategoryAPI.dll"]
