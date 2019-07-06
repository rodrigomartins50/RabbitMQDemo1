FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["src/RabbitMQDemo1.Microservice/RabbitMQDemo1.Microservice.csproj", "src/RabbitMQDemo1.Microservice/"]
RUN dotnet restore "src/RabbitMQDemo1.Microservice/RabbitMQDemo1.Microservice.csproj"
COPY . .
WORKDIR "/src/src/RabbitMQDemo1.Microservice"
RUN dotnet build "RabbitMQDemo1.Microservice.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "RabbitMQDemo1.Microservice.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "RabbitMQDemo1.Microservice.dll"]
