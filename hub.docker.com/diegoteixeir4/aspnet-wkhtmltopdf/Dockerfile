FROM mcr.microsoft.com/dotnet/core/aspnet:2.2

RUN apt update -y && \
    apt install -y fontconfig fontconfig-config fonts-dejavu-core libbsd0 libexpat1 \
    libfontconfig1 libfontenc1 libfreetype6 libjpeg62-turbo libpng16-16 libx11-6 libx11-data \
    libxau6 libxcb1 libxdmcp6 libxext6 libxfont1 libxrender1 ucf x11-common xfonts-75dpi \
    xfonts-base xfonts-encodings xfonts-utils && \
    apt install -y xvfb && \
    curl -L https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.5/wkhtmltox_0.12.5-1.stretch_amd64.deb -o /tmp/wkhtmltox_0.12.5-1.stretch_amd64.deb && \
    dpkg -i /tmp/wkhtmltox_0.12.5-1.stretch_amd64.deb
