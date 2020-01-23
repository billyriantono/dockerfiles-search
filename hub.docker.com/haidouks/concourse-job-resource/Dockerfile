FROM mcr.microsoft.com/powershell:6.2.3-alpine-3.8
RUN pwsh -c "Get-PSRepository"
RUN pwsh -c "Install-Module concourse -Verbose"
RUN mkdir -p /opt/resource 
ADD assets/* /opt/resource/
RUN chmod +x /opt/resource/*
WORKDIR /opt/resource
