FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build-env

ENV TZ 'America/Chicago'
RUN apt-get update && apt-get install -y tzdata 
RUN mkdir -p /config/etc && mv /etc/timezone /config/etc/ && ln -s /config/etc/timezone /etc/
RUN dpkg-reconfigure -f noninteractive tzdata
RUN echo $TZ > /config/etc/timezone

WORKDIR /app
COPY ./ ./
RUN ls -la

RUN dotnet restore
RUN dotnet publish -c Release -o out ./TeaLeaves.Web/TeaLeaves.Web.csproj

    
# build runtime image

FROM mcr.microsoft.com/dotnet/core/aspnet:2.2
WORKDIR /app
COPY --from=build-env /app/TeaLeaves.Web/out ./

ENTRYPOINT ["dotnet", "TeaLeaves.Web.dll"]
