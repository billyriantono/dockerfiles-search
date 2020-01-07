FROM microsoft/nanoserver

WORKDIR C:/minio
RUN mkdir data config
RUN powershell "Invoke-WebRequest -Uri https://dl.minio.io/server/minio/release/windows-amd64/minio.exe -OutFile minio.exe"
VOLUME [ "C:/minio/data", "C:/minio/config" ]
EXPOSE 9000
ENTRYPOINT [ "C:/minio/minio.exe" ]
CMD [ "server" , "--config-dir" , "config" , "data" ]
