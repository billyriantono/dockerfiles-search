FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY src/DeadInsect.Microservice.Link.Api/DeadInsect.Microservice.Link.Api.csproj src/DeadInsect.Microservice.Link.Api/
COPY src/DeadInsect.Microservice.Link.Application/DeadInsect.Microservice.Link.Application.csproj src/DeadInsect.Microservice.Link.Application/
COPY src/DeadInsect.Microservice.Link.Data/DeadInsect.Microservice.Link.Data.csproj src/DeadInsect.Microservice.Link.Data/
RUN dotnet restore src/DeadInsect.Microservice.Link.Api/DeadInsect.Microservice.Link.Api.csproj
COPY . .
WORKDIR /src/src/DeadInsect.Microservice.Link.Api
RUN dotnet build DeadInsect.Microservice.Link.Api.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish DeadInsect.Microservice.Link.Api.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DeadInsect.Microservice.Link.Api.dll"]
