FROM rocker/rstudio:latest

LABEL maintainer="Ilan Gofer"
ENV DEBIAN_FRONTEND noninteractive

WORKDIR /workspace/
COPY . .

RUN cp debian.list /etc/apt/sources.list.d
RUN apt update
RUN apt-get install -y \
                    apt-utils \
                    git \
                    build-essential \
                    wget \
                    htop \
                    nano \
                    openssl libssl-dev \
                    libcairo2 \
                    libcairo2-dev \
                    libcurl4-openssl-dev \
                    unixodbc* \
                    unixodbc-dev \
                    r-cran-rodbc \
                    freetds-bin \
                    freetds-common \
                    tdsodbc \
                    libxt-dev libgtk2.0-dev xvfb xauth xfonts-base \
                    libxml2-dev \
                    default-jre \
                    openjdk-8-jdk \
                    multiarch-support \
                    r-cran-rjava \
                    freetds-dev \
                    libudunits2-dev \
                    gfortran \
                     wget \
                    libxtst6 \
                    default-jre \
                    curl
RUN apt-get install -y unixodbc*
RUN apt-get install -y unixodbc-dev

RUN wget --quiet https://repo.anaconda.com/archive/Anaconda3-2019.03-Linux-x86_64.sh -O ~/anaconda.sh && /bin/bash ~/anaconda.sh -b -p /opt/conda && rm ~/anaconda.sh && ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh && echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc && echo "conda activate base" >> ~/.bashrc
RUN /opt/conda/bin/pip install -r requirements.txt
RUN wget http://download.jetbrains.com/python/pycharm-community-2019.1.3.tar.gz
RUN tar -xzf pycharm-community-2019.1.3.tar.gz
RUN rm pycharm-community-2019.1.3.tar.gz
# RUN rm Anaconda3-2019.03-Linux-x86_64.sh
RUN Rscript packages.r
