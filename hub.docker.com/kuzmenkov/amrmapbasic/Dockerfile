FROM ubuntu:bionic

RUN useradd docker \
	&& mkdir /home/docker \
	&& chown -R docker:docker /home/docker \
	&& addgroup docker staff
RUN apt update \
	&& apt install -y locales \	
	&& echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen \
	&& locale-gen en_US.utf8 \
	&& /usr/sbin/update-locale LANG=en_US.UTF-8
ENV LC_ALL en_US.UTF-8
ENV LANG en_US.UTF-8

## Install some useful tools and dependencies for MRO
RUN apt update \
	&& apt install -y --no-install-recommends \
	apt-utils \
	ca-certificates \
	curl \
        wget \
	&& rm -rf /var/lib/apt/lists/*

# system libraries of general use
RUN apt update && apt install -y \
    sudo \
    pandoc \
    pandoc-citeproc \
    libcurl4-gnutls-dev \
    libcairo2-dev \
    libxt-dev \
    libssl-dev \
    libssh2-1-dev \
    libssl1.0.0 \
    libxml2-dev \
    gdebi \
    libssl-dev\
    libmpfr-dev \
    gfortran \
    aptitude \
    libgdal-dev \
    libproj-dev \
    g++ \
    libicu-dev \
    libpcre3-dev\
    libbz2-dev \
    liblzma-dev \
    libnlopt-dev \
    build-essential \
    && rm -rf /var/lib/apt/lists/*
    
WORKDIR /home/docker
RUN sudo wget https://mirrors.kernel.org/ubuntu/pool/main/libp/libpng/libpng12-0_1.2.54-1ubuntu1_amd64.deb \
&& dpkg -i libpng12-0_1.2.54-1ubuntu1_amd64.deb \
# Download, valiate, and unpack and install Micrisift R open
&& wget https://www.dropbox.com/s/uz4e4d0frk21cvn/microsoft-r-open-3.5.1.tar.gz?dl=1 -O microsoft-r-open-3.5.1.tar.gz \
&& echo "9791AAFB94844544930A1D896F2BF1404205DBF2EC059C51AE75EBB3A31B3792 microsoft-r-open-3.5.1.tar.gz" > checksum.txt \
	&& sha256sum -c --strict checksum.txt \
	&& tar -xf microsoft-r-open-3.5.1.tar.gz \
	&& cd /home/docker/microsoft-r-open \
	&& ./install.sh -a -u \
	&& ls logs && cat logs/* \
	&& cd /home/docker \
	&& rm microsoft-r-open-3.5.1.tar.gz \
	&& rm checksum.txt \
	&& rm -r microsoft-r-open


#COPY Makeconf /usr/lib64/microsoft-r/3.3/lib64/R/etc/Makeconf

RUN apt install -y software-properties-common \
&& add-apt-repository -y ppa:ubuntugis/ubuntugis-unstable \
&& apt update && apt install -y \
libudunits2-dev \
libgdal-dev \
libgeos-dev openjdk-11-jdk \
&& java -version \
&& rm -rf /var/lib/apt/lists/*
#RUN sudo apt-add-repository -y ppa:webupd8team/java \
#&& apt update && echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 select true" | sudo debconf-set-selections && apt-get install -y oracle-java8-installer \
#&& R -e "Sys.setenv(JAVA_HOME = '/usr/lib/jvm/java-8-oracle/jre')"
#RUN sudo java -version

# basic shiny functionality
RUN R -e "install.packages('binom', repos='https://cran.r-project.org/')" \
&& R -e "install.packages('dplyr', repos='https://cran.r-project.org/')" \
&& R -e "install.packages(c('shiny', 'rmarkdown'), repos='https://cran.r-project.org/')" \
&& R -e "install.packages('ggplot2', repos='https://cran.r-project.org/')" \
&& R -e "install.packages('reshape', repos='https://cran.r-project.org/')" \
&& R -e "install.packages('curl', repos='https://cran.r-project.org/')" \
&& R -e "install.packages('httr', repos='https://cran.r-project.org/')" \
&& R -e "install.packages('devtools', repos='https://cran.r-project.org/')" \
&& R -e "install.packages('remotes', repos='https://cran.r-project.org/')" \
#&& R -e "remotes::install_url('https://cran.r-project.org/src/contrib/httpuv_1.4.3.tar.gz')" \
#&& R -e "download.file('https://github.com/rstudio/httpuv/archive/master.zip', 'httpuv-master.zip'); unlink('httpuv-master', recursive = TRUE); unzip('httpuv-master.zip', unzip = '/usr/bin/unzip'); file.mode('httpuv-master/src/libuv/configure')" \
#&& R -e "options(unzip = 'internal'); options(unzip = '/usr/bin/unzip'); devtools::install_github('rstudio/httpuv')" \
#&& R -e "options(unzip = 'internal'); devtools::install_github('rstudio/shiny')" \
&& R -e "install.packages('formattable', repos='https://cran.r-project.org/')" \
&& R -e "install.packages('car', repos='https://cran.r-project.org/')" \
&& R -e "install.packages('fmsb', repos='https://cran.r-project.org/')" \
&& R -e "install.packages('igraph', repos='https://cran.r-project.org/')" \
&& R -e "install.packages(с('miniUI', 'shinyjs'), repos='https://cran.r-project.org/')" \
#&& sudo su - -c "R -e \"install.packages('miniUI', repos='https://cran.r-project.org/');options(unzip = 'internal'); remotes::install_github('daattali/shinyjs')\"" \
#RUN R -e "options(unzip = 'internal'); devtools::install_github('daattali/shinyjs')" \
&& R -e "install.packages('scales', repos='https://cran.r-project.org/')" \
&& R -e "install.packages('crosstalk', repos='https://cran.r-project.org/')" \
&& R -e "install.packages('DT', repos='https://cran.r-project.org/')" \
#&& sudo su - -c "R -e \"options(unzip = 'internal'); remotes::install_github('rstudio/DT')\"" \
#RUN R -e "devtools::install_github('rstudio/DT')" \
&& R -e "install.packages(c('raster', 'sp', 'viridis', 'leaflet', 'leaflet.extras'), repos='https://cran.r-project.org/')" \
#&& sudo su - -c "R -e \"install.packages(c('raster', 'sp', 'viridis', 'leaflet'), repos='https://cran.r-project.org/');options(unzip = 'internal'); remotes::install_github('rstudio/leaflet')\"" \
#&& sudo su - -c "R -e \"options(unzip = 'internal'); remotes::install_github('bhaskarvk/leaflet.extras')\"" \
&& R -e "install.packages('ggrepel', repos='https://cran.r-project.org/')" \
#RUN R -e "install.packages('leaflet', repos='https://cran.r-project.org/')" \
&& R -e "install.packages('visNetwork', repos='https://cran.r-project.org/')" \
&& R -e "install.packages('purrr', repos='https://cran.r-project.org/')" \
&& sudo su - -c "R -e \"remotes::install_git('https://github.com/kuzmenkov111/highcharter')\""
#&& sudo su - -c "R -e \"options(unzip = 'internal'); remotes::install_github('kuzmenkov111/highcharter')\"" 


