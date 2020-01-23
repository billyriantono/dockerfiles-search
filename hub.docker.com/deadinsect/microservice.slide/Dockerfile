FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY src/DeadInsect.Microservice.Slide.Api/DeadInsect.Microservice.Slide.Api.csproj src/DeadInsect.Microservice.Slide.Api/
COPY src/DeadInsect.Microservice.Slide.Application/DeadInsect.Microservice.Slide.Application.csproj src/DeadInsect.Microservice.Slide.Application/
COPY src/DeadInsect.Microservice.Slide.Data/DeadInsect.Microservice.Slide.Data.csproj src/DeadInsect.Microservice.Slide.Data/
RUN dotnet restore src/DeadInsect.Microservice.Slide.Api/DeadInsect.Microservice.Slide.Api.csproj
COPY . .
WORKDIR /src/src/DeadInsect.Microservice.Slide.Api
RUN dotnet build DeadInsect.Microservice.Slide.Api.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish DeadInsect.Microservice.Slide.Api.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DeadInsect.Microservice.Slide.Api.dll"]
