FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["MS-BlazorApp/MS-BlazorApp.csproj", "MS-BlazorApp/"]
RUN dotnet restore "MS-BlazorApp/MS-BlazorApp.csproj"
COPY . .
WORKDIR "/src/MS-BlazorApp"
RUN dotnet build "MS-BlazorApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MS-BlazorApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MS-BlazorApp.dll"]
