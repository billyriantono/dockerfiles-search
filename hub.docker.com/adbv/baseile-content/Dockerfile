FROM mcr.microsoft.com/dotnet/core/sdk:2.2

RUN curl -sL https://deb.nodesource.com/setup_6.x | bash - \
    && apt-get install -y nodejs \
    && npm install -g bower gulp \
    && groupadd -g 1001 build \
    && useradd -m -u 1001 -g build build
