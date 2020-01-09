FROM rocker/r-ver:3.3.1

WORKDIR /tmp

RUN apt-get update -y && apt-get install -y \
	libssl-dev \
	libcurl3 \
	libcurl4-openssl-dev \
	curl \
	libxml2-dev \
	pkg-config \
	libcairo2-dev \
	libsqlite-dev \
	libssh2-1-dev \
	liblzma5 \
	liblzma-dev \
	libbz2-1.0 \
	libbz2-dev \
	unzip \
	zip \
	gzip \
	libpcre3 \
	libicu52 \
	libicu-dev \
	openjdk-7-jdk


COPY Rprofile.site /usr/local/lib/R/etc/Rprofile.site

COPY install_pkgs.R .
RUN R -f install_pkgs.R

CMD ["R"]
