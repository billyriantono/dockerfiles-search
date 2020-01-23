FROM mcr.microsoft.com/dotnet/core/runtime:2.2.4-alpine3.9

RUN apk add python curl
RUN curl -O https://bootstrap.pypa.io/get-pip.py; python get-pip.py

RUN pip install awscli --upgrade
