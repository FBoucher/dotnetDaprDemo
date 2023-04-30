FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /
COPY testapp.csproj .
RUN dotnet restore testapp.csproj
COPY . .
RUN dotnet build testapp.csproj -c Release -o /app/build

FROM build AS publish
RUN dotnet publish testapp.csproj -c Release -o /app/publish

FROM nginx:alpine AS final
WORKDIR /usr/share/nginx/html
EXPOSE 80
EXPOSE 443
COPY --from=publish /app/publish/wwwroot .
COPY nginx.conf /etc/nginx/nginx.conf