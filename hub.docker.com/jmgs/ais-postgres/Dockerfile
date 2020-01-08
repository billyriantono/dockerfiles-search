#Run from solution root folder (../..) with the following cmd:
#docker build -t ADCPostgre:TAG -f src\ADC.PostgreClient\Dockerfile .

FROM mcr.microsoft.com/dotnet/core/runtime:2.2 as base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:2.2 as build
WORKDIR /srcdir
COPY . ./
RUN dotnet restore --configfile NuGet.config
RUN dotnet publish src/ADC.PostgreClient -c Release -o /app 

FROM base AS final
WORKDIR /app
COPY --from=build /app .
ENTRYPOINT ["dotnet", "ADC.PostgreClient.dll"]


