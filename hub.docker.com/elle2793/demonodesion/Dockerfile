FROM mcr.microsoft.com/dotnet/core/sdk:2.2

LABEL mantainer="Elio Severo Junior <elioseverojunior@gmail.com>"
LABEL Description="Docker DotNet GitVersion"

ENV JENKINS_BUILD_NUMBER=0
ENV PATH="PATH=$PATH:/root/.dotnet/tools:$PATH"

WORKDIR /pre-build

RUN apt-get update \
  && apt-get install -y jq tree exiftool \
  && rm -rf /var/lib/apt/lists/*

RUN dotnet tool install --global GitVersion.Tool

RUN echo "alias gitversion=\"/root/.dotnet/tools/dotnet-gitversion\"" >> ~/.bash_profile
RUN /bin/bash -c "source ~/.bash_profile"
