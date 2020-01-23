# Stage 1
FROM mcr.microsoft.com/dotnet/core-nightly/sdk:2.2 as build
WORKDIR /app

COPY src src
RUN dotnet build src/IssueMl.Web

# Stage 2
FROM build as publish
WORKDIR /app

RUN dotnet publish src/IssueMl.Web -c Release -o /app -r linux-x64

# Stage 3
FROM mcr.microsoft.com/dotnet/core-nightly/runtime:2.2 AS runtime

ENV DOTNET_USE_POLLING_FILE_WATCHER=true
# ENV PORT=443
# ENV ASPNETCORE_URL=https://+:${PORT}
ENV Kestrel__Certificates__Default__Path=/app/Cert/cert-aspnetcore.pfx
ENV Kestrel__Certificates__Default__Password=1234

WORKDIR /app
COPY --from=publish /app .

CMD dotnet IssueMl.Web.dll --urls https://+:443