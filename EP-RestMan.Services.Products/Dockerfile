FROM microsoft/aspnetcore:2.0-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0-nanoserver-1709 AS build
WORKDIR /src
COPY EP-RestMan.Services.Products/EP-RestMan.Services.Products.csproj EP-RestMan.Services.Products/
RUN dotnet restore EP-RestMan.Services.Products/EP-RestMan.Services.Products.csproj
COPY . .
WORKDIR /src/EP-RestMan.Services.Products
RUN dotnet build EP-RestMan.Services.Products.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish EP-RestMan.Services.Products.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "EP-RestMan.Services.Products.dll"]
