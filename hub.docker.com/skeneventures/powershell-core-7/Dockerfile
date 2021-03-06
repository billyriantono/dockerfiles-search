# Copyright (c) Microsoft Corporation. All rights reserved.
# Licensed under the MIT License.

# Docker image file based on:
#    https://github.com/PowerShell/PowerShell-Docker/blob/master/release/stable/alpine/docker/Dockerfile

# Define arg(s) needed for the From statement
ARG fromTag=latest
ARG imageRepo=alpine

FROM ${imageRepo}:${fromTag} AS installer-env

# Define Args for the needed to add the package
ARG PS_VERSION=7.0.0-rc.1
ARG PS_PACKAGE=powershell-${PS_VERSION}-linux-alpine-x64.tar.gz
ARG PS_PACKAGE_URL=https://github.com/PowerShell/PowerShell/releases/download/v${PS_VERSION}/${PS_PACKAGE}
ARG PS_INSTALL_VERSION=7

# Download the Linux tar.gz and save it
ADD ${PS_PACKAGE_URL} /tmp/linux.tar.gz

# define the folder we will be installing PowerShell to
ENV PS_INSTALL_FOLDER=/opt/microsoft/powershell/$PS_INSTALL_VERSION

# Create the install folder
RUN mkdir -p ${PS_INSTALL_FOLDER}

# Unzip the Linux tar.gz
RUN tar zxf /tmp/linux.tar.gz -C ${PS_INSTALL_FOLDER}

# Start a new stage so we lose all the tar.gz layers from the final image
FROM ${imageRepo}:${fromTag}

# Copy only the files we need from the previous stage
COPY --from=installer-env ["/opt/microsoft/powershell", "/opt/microsoft/powershell"]

# Define Args and Env needed to create links
ARG PS_INSTALL_VERSION=7
ENV PS_INSTALL_FOLDER=/opt/microsoft/powershell/$PS_INSTALL_VERSION \
    \
    # Define ENVs for Localization/Globalization
    DOTNET_SYSTEM_GLOBALIZATION_INVARIANT=false \
    LC_ALL=en_US.UTF-8 \
    LANG=en_US.UTF-8 \
    # set a fixed location for the Module analysis cache
    PSModuleAnalysisCachePath=/var/cache/microsoft/powershell/PSModuleAnalysisCache/ModuleAnalysisCache

# Install dotnet dependencies and ca-certificates
RUN apk add --no-cache \
    ca-certificates \
    less \
    \
    # PSReadline/console dependencies
    ncurses-terminfo-base \
    \
    # .NET Core dependencies
    krb5-libs \
    libgcc \
    libintl \
    libssl1.1 \
    libstdc++ \
    tzdata \
    userspace-rcu \
    zlib \
    icu-libs \
    && apk -X https://dl-cdn.alpinelinux.org/alpine/edge/main add --no-cache \
    lttng-ust \
    \
    # Create the pwsh symbolic link that points to powershell
    && ln -s ${PS_INSTALL_FOLDER}/pwsh /usr/bin/pwsh \
    # Give all user execute permissions and remove write permissions for others
    && chmod a+x,o-w ${PS_INSTALL_FOLDER}/pwsh \
    # intialize powershell module cache
    && pwsh \
        -NoLogo \
        -NoProfile \
        -Command " \
          \$ErrorActionPreference = 'Stop' ; \
          \$ProgressPreference = 'SilentlyContinue' ; \
          while(!(Test-Path -Path \$env:PSModuleAnalysisCachePath)) {  \
            Write-Host "'Waiting for $env:PSModuleAnalysisCachePath'" ; \
            Start-Sleep -Seconds 6 ; \
          }" \
    # extra folders for mounting and module loading
    && mkdir -p /opt/shared/powershell \
    && mkdir -p /root/.config/powershell/ \
    && echo '$Env:PSModulePath += ":/opt/shared/powershell/Modules"' > /root/.config/powershell/Microsoft.PowerShell_profile.ps1

# Define args needed only for the labels
ARG PS_VERSION=7.0.0-rc.1
ARG IMAGE_NAME=skeneventures/powershell-core-7:latest
ARG VCS_REF="none"

# Add label last as it's just metadata and uses a lot of parameters
LABEL maintainer="Martyn Skene Ashworth <martyn@skven.io>" \
    readme.md="https://github.com/skene-ventures/docker-images/blob/master/README.md" \
    description="This Dockerfile will install the latest release of PowerShell." \
    org.label-schema.usage="https://github.com/PowerShell/PowerShell/tree/master/docker#run-the-docker-image-you-built" \
    org.label-schema.url="https://github.com/skene-ventures/docker-powershell-core-7/blob/master/README.md" \
    org.label-schema.vcs-url="https://github.com/PowerShell/PowerShell-Docker" \
    org.label-schema.name="powershell" \
    org.label-schema.vendor="PowerShell" \
    org.label-schema.vcs-ref=${VCS_REF} \
    org.label-schema.version=${PS_VERSION} \
    org.label-schema.schema-version="1.0" \
    org.label-schema.docker.cmd="docker run ${IMAGE_NAME} pwsh -c '$psversiontable'" \
    org.label-schema.docker.cmd.devel="docker run ${IMAGE_NAME}" \
    org.label-schema.docker.cmd.test="docker run ${IMAGE_NAME} pwsh -c Invoke-Pester" \
    org.label-schema.docker.cmd.help="docker run ${IMAGE_NAME} pwsh -c Get-Help"

CMD [ "pwsh" ]
