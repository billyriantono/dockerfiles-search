FROM microsoft/dotnet:2.2.1-aspnetcore-runtime    
    
RUN apt-get update -y \
    && apt-get install -y \
            fontconfig \
            libfreetype6 \
            libjpeg62-turbo \
            libpng16-16 \
            libx11-6 \
            libxcb1 \
            libxext6 \
            libxrender1 \
            xfonts-75dpi \
            xfonts-base \
            wget \
    && wget https://downloads.wkhtmltopdf.org/0.12/0.12.5/wkhtmltox_0.12.5-1.stretch_amd64.deb \
    && dpkg -i wkhtmltox_0.12.5-1.stretch_amd64.deb \
    && chmod +x /usr/local/bin/wkhtmltopdf \
	&& chmod +x /usr/local/bin/wkhtmltoimage