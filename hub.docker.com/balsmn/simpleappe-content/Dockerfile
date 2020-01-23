FROM debian:buster

# common build tools
RUN apt-get -y update && \
    apt-get -y upgrade && \
    apt-get -y install git make gcc pkg-config autoconf

# pull imagemagick source and install various dependencies including pango and emoji font;
# curl is used by imagemagick https delegate
RUN apt-get -y install curl ghostscript fonts-noto-color-emoji libmagickwand-dev libpango1.0-dev 
RUN git clone https://github.com/ImageMagick/ImageMagick.git && \
    cd ImageMagick && git checkout 7.0.8-61

# apply patches and build imagemagick from source
COPY pango-spacing.patch ImageMagick/
RUN cd ImageMagick && git apply pango-spacing.patch && \
    ./configure && make && make install && \
    ldconfig /usr/local/lib

# apache interface for imagemagick renderers with cgi module enabled
RUN apt-get -y install apache2 && \
    a2enmod cgid

# copy app source
WORKDIR /app
COPY . /app/

# link app resources
RUN ln -s /app/public/fonts/* /usr/share/fonts/truetype/ && \
    rm -rf /usr/lib/cgi-bin /var/www/html && \
    ln -s /app/cgi-bin /usr/lib/cgi-bin && \
    ln -s /app/public /var/www/html

# development tools
RUN apt-get -y install inotify-tools ruby

EXPOSE 80
CMD ["apachectl", "-D", "FOREGROUND"]
