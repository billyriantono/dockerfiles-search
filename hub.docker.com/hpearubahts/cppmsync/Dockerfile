FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build-env
WORKDIR /app
RUN apt-get update && apt-get install -y curl gnupg2
RUN curl -sL https://deb.nodesource.com/setup_11.x  | bash -
RUN apt-get -y install nodejs
COPY *.csproj ./
RUN dotnet restore
COPY . ./
RUN dotnet publish -c Release -r ubuntu.16.10-x64 -o out

FROM ubuntu:latest
# Add the PostgreSQL PGP key to verify their Debian packages. It should be the same key as https://www.postgresql.org/media/keys/ACCC4CF8.asc
RUN apt-get update && apt-get install -y curl gnupg2 supervisor 
RUN apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys B97B0AFCAA1A47F044F244A07FCC7D46ACCC4CF8
RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ precise-pgdg main" > /etc/apt/sources.list.d/pgdg.list
RUN apt-get update && apt-get install -y software-properties-common postgresql-10 postgresql-client-10 postgresql-contrib-10 dos2unix
RUN curl -sL https://deb.nodesource.com/setup_11.x  | bash -
RUN apt-get -y install nodejs

USER postgres
RUN    /etc/init.d/postgresql start &&\
    psql --command "CREATE USER cppmsync WITH SUPERUSER PASSWORD 'cppmsync';" &&\
    createdb -O cppmsync cppmsync && \
	/etc/init.d/postgresql stop
RUN echo "host all  all    0.0.0.0/0  md5" >> /etc/postgresql/10/main/pg_hba.conf
RUN echo "listen_addresses='*'" >> /etc/postgresql/10/main/postgresql.conf

USER root
WORKDIR /CPPMSync
COPY --from=build-env /app/out .
RUN ["chmod", "+x", "/CPPMSync/CPPMSync"]
RUN ["chmod", "+x", "/CPPMSync/startup.sh"]
RUN ["rm", "-f", "/CPPMSync/appsettings.json"]
RUN ["rm", "-f", "/CPPMSync/HTTPCertificate.pfx"]
RUN ["dos2unix", "startup.sh"]
#COPY ./appsettings.defaults.json ./appsettings.json
COPY ./ArubaHTS.pem /usr/local/share/ca-certificates/ArubaHTS.crt
COPY ./ArubaHTS-Licensing.pem /usr/local/share/ca-certificates/ArubaHTS-Licensing.crt
RUN chmod 644 /usr/local/share/ca-certificates/ArubaHTS.crt && \
	chmod 644 /usr/local/share/ca-certificates/ArubaHTS-Licensing.crt && \
	update-ca-certificates

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
#VOLUME  ["/etc/postgresql", "/var/log/postgresql", "/var/lib/postgresql"]
CMD export ASPNETCORE_AppSettings__ClearPassApiUrl=$API_URL && \
    echo ASPNETCORE_AppSettings__ClearPassApiUrl=$ASPNETCORE_AppSettings__ClearPassApiUrl && \
    export ASPNETCORE_AppSettings__ClearPassApiToken=$API_ACCESS_TOKEN && \
    echo ASPNETCORE_AppSettings__ClearPassApiToken=$ASPNETCORE_AppSettings__ClearPassApiToken && \
    export ASPNETCORE_AppSettings__ClearPassHostFQDN=$EXTENSION_PLATFORM_FQDN && \
    echo ASPNETCORE_AppSettings__ClearPassHostFQDN=$ASPNETCORE_AppSettings__ClearPassHostFQDN && \
    export ASPNETCORE_AppSettings__ClearPassHostInstance=$EXTENSION_INSTANCE_ID && \
    echo ASPNETCORE_AppSettings__ClearPassHostInstance=$ASPNETCORE_AppSettings__ClearPassHostInstance && \
    export ASPNETCORE_AppSettings__ClearPassHostIP=$EXTENSION_HOST_IP && \
    echo ASPNETCORE_AppSettings__ClearPassHostIP=$ASPNETCORE_AppSettings__ClearPassHostIP && \
	/CPPMSync/startup.sh

LABEL \
 com.hpe.aruba.clearpass.extension.name="CPPMSync" \
 com.hpe.aruba.clearpass.extension.version="0.10.2" \
 com.hpe.aruba.clearpass.extension.icon.href="https://hpearubahts.bitbucket.io/cppmsync-icon-256.png" \
 com.hpe.aruba.clearpass.extension.description="Multiple ClearPass Cluster Replication and Synchronization" \
 com.hpe.aruba.clearpass.extension.singleton=true \
 com.hpe.aruba.clearpass.extension.api.access=true \
 com.hpe.aruba.clearpass.extension.restart="unless-stopped" \ 
 com.hpe.aruba.clearpass.extension.publish.ports="yes" \ 
 com.hpe.aruba.clearpass.extension.ports.tcp.4050="4050" \
 com.hpe.aruba.clearpass.extension.ports.tcp.4050.description="CPPMSync Web UI (HTTP)" \
 com.hpe.aruba.clearpass.extension.ports.tcp.4051="4051" \
 com.hpe.aruba.clearpass.extension.ports.tcp.4051.description="CPPMSync Web UI (HTTPS)" \
 com.hpe.aruba.clearpass.extension.ports.udp.8514="8514" \
 com.hpe.aruba.clearpass.extension.ports.udp.8514.description="Syslog (UDP) Receiver for Event Processing" \
 com.hpe.aruba.clearpass.extension.ports.tcp.8514="8514" \
 com.hpe.aruba.clearpass.extension.ports.tcp.8514.description="Syslog (TCP) Receiver for Event Processing" \
 com.hpe.aruba.clearpass.extension.logs="/app/log" \
 com.hpe.aruba.clearpass.extension.config.format="json" \
 com.hpe.aruba.clearpass.extension.config.file="/CPPMSync/appsettings.json" \
 com.hpe.aruba.clearpass.extension.files.License="/CPPMSync/CustomerLicense.pem" \
 com.hpe.aruba.clearpass.extension.files.HTTPSCert="/CPPMSync/HTTPSCertificate.pem" \
 com.hpe.aruba.clearpass.extension.files.HTTPSCertKey="/CPPMSync/HTTPSCertificate.key" \
 com.hpe.aruba.clearpass.extension.config.defaults="{\"AppSettings\": {\"JwtLoginSecret\": \"YUVVYBREQZMDJIGJPWDANNFNDVDOFWDJBCYZIUGJOCXCNGNVVN\",\"PassEncryptionKey\": \"~{A+r!PZ5TykWtUV\"},\"Logging\": {\"LogLevel\": {\"Default\": \"Information\" }  }}" 
#com.hpe.aruba.clearpass.extension.config.defaults="/CPPMSync/appsettings.defaults.json"

EXPOSE 4050
EXPOSE 4051
EXPOSE 8514

ENV ASPNETCORE_URLS http://+:4050;https://+:4051