FROM microsoft/dotnet:2.2-sdk as builder  
ENV DOTNET_CLI_TELEMETRY_OPTOUT 1

RUN mkdir -p /root/src/app  
WORKDIR /root/src/app

COPY LaCimbaliJuniorRaspiService     LaCimbaliJuniorRaspiService
WORKDIR /root/src/app/LaCimbaliJuniorRaspiService

RUN dotnet restore ./LaCimbaliJuniorRaspiService.csproj
RUN dotnet publish -c release -o published -r linux-arm

FROM  microsoft/dotnet:2.2-runtime-stretch-slim-arm32v7

WORKDIR /root/

COPY --from=builder /root/src/app/LaCimbaliJuniorRaspiService/published .
COPY ./version.json . 

CMD ["dotnet", "./LaCimbaliJuniorRaspiService.dll"]