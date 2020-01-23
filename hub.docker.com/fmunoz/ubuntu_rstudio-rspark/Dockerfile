FROM rocker/rstudio:3.3.2
MAINTAINER "Felipe de Jesus Muñoz Gonzalez" fmunoz@lcg.unam.mx

RUN echo en_US.UTF-8 UTF-8 >> /etc/locale.gen && \
    locale-gen && \
    update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8

ENV LANG en_US.UTF-8  
ENV LANGUAGE en_US:en  
ENV LC_ALL en_US.UTF-8

RUN apt-get -y -q dist-upgrade 

#RUN apt-get -y update -qq  && apt-get -y upgrade

#RUN apt-get install -y --no-install-recommends apt-utils  software-properties-common 

#RUN sudo add-apt-repository -y ppa:ubuntu-toolchain-r/test 

RUN apt-get -y update -qq  && apt-get -y upgrade

RUN apt-get install -y --no-install-recommends \
    libpangoft2-1.0-0  \
    libxt-dev \
    xvfb \
    xauth \ 
    xfonts-base \
    libglib2.0-0  \
    libglib2.0-bin  \
    libpango-1.0-0  \
    libxml2-dev \
    libglib2.0-dev \
    libgdk-pixbuf2.0-dev \
    libatk1.0-dev \
    libssl1.0.0  \
    libpangocairo-1.0-0 \
    libcairo2  \
    libcairo2-dev \ 
    fonts-dejavu \
    gfortran \
    libssh2-1-dev \
    r-cran-xml \
    r-cran-plyr \ 
    r-cran-ggplot2 \
    r-cran-gplots \    
    libnlopt-dev \
    xml-core \
    lsb-release \
    libssl-dev \
    libbz2-dev \
    libpcre3-dev \
    liblzma-dev \
    libicu-dev \
    libssl-dev  \
    libcurl4-openssl-dev \
    glibc-source \
    openjdk-8*  \
    openjdk-9* \
    gcc && apt-get clean
    


# Install SparkR

WORKDIR /home/root
RUN wget https://cran.r-project.org/src/contrib/rJava_0.9-8.tar.gz
RUN R CMD INSTALL rJava_0.9-8.tar.gz
RUN R CMD javareconf


RUN Rscript -e "install.packages(c('sparklyr','nycflights13', 'Lahman'), repos='https://cloud.r-project.org')"


RUN groupadd rstudio
RUN useradd -g rstudio rstudio
RUN echo rstudio | passwd --stdin rstudio

EXPOSE 8787
CMD /usr/lib/rstudio-server/bin/rserver --server-daemonize 0
