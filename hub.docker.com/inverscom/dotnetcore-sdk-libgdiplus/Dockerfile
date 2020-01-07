FROM mcr.microsoft.com/dotnet/core/sdk:2.2

RUN apt-get update \
    && apt-get install -y libgdiplus libc6-dev unzip \
    && ln -s /usr/lib/libgdiplus.so /usr/lib/gdiplus.dll
