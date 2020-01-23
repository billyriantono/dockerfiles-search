FROM mcr.microsoft.com/powershell:latest AS powershell
COPY . /app
VOLUME /conf
ENTRYPOINT ["/opt/microsoft/powershell/6/pwsh", "-f /app/init.ps1"]
