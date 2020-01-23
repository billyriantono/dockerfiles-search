#########
#
#     Dockerfile for Metabolomics Course
#
### To run the container for the first time with generic graphics:
# xhost +
# docker run -it --rm -v /tmp/.X11-unix:/tmp/.X11-unix:rw --privileged -e DISPLAY=unix$DISPLAY \
# -v $HOME/:/home/training/ --device /dev/dri --privileged --name metabolomics ebitraining/metabolomics
#
## To run with Nvidia graphics, add the following option:
# "-v /usr/lib/nvidia-340:/usr/lib/nvidia-340 -v /usr/lib32/nvidia-340:/usr/lib32/nvidia-340"
#
### To resume using an container:
# docker exec -it metabolomics /bin/bash
#
### To build the container:
# docker build -f ./Dockerfile -t metabolomics .
# docker tag metabolomics ebitraining/metabolomics:latest
# docker push ebitraining/metabolomics:latest
#
#########

FROM ubuntu:18.04
LABEL author="Mohamed Alibi" \
description="Docker image for Metabolomics Course" \
maintainer="Mohamed Alibi <alibi@ebi.ac.uk>"

# Pre requirements
########
RUN rm /bin/sh && ln -s /bin/bash /bin/sh
ENV DEBIAN_FRONTEND noninteractive
ENV LC_ALL en_GB.UTF-8
ENV LANG en_GB.UTF-8
ENV LANGUAGE en_GB:en

RUN apt-get update \
    && apt-get -y upgrade \
    && apt-get install -y --reinstall language-pack-en \
    && apt-get install -y gnupg gdebi expect \
    && locale-gen en_GB.UTF-8

ADD https://download1.rstudio.org/rstudio-xenial-1.1.456-amd64.deb /usr/local/rstudio.deb
RUN echo "deb http://cloud.r-project.org/bin/linux/ubuntu bionic-cran35/" >> /etc/apt/sources.list \
    && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9

RUN apt-get update; apt-get install -y build-essential ca-certificates libbz2-dev liblzma-dev gfortran \
    libncurses5-dev libncursesw5-dev zlib1g-dev automake pkg-config unzip openjdk-8-jre-headless cmake \
    git wget sudo autoconf make xml2 locales libjpeg-dev zlibc libjpeg62 libxslt1.1 nano openjdk-8-jre \
    libxcomposite1 libtiff5 libqt5widgets5 libqt5webkit5 libssl-dev python3 mesa-common-dev libxml2-dev \
    libcurses-ocaml-dev libgl1-mesa-dri libgl1-mesa-glx mesa-utils fcitx-frontend-qt5 libqt5gui5 gdebi \
    fcitx-modules fcitx-module-dbus libedit2 libqt5core5a libqt5dbus5 libqt5network5 libqt5printsupport5 \
    default-jre default-jre-headless expect libcurl4 libcurl4-openssl-dev curl libssh2-1-dev \
    libopenblas-base libgsl-dev liblapacke liblapacke-dev libncurses-dev patch libnetcdf-dev \
    openssl libssl-dev libmysqlclient-dev libpng-dev manpages vim libopenblas-dev netcdf-bin libapparmor-dev \
    && update-alternatives --set java /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java \
    && echo "en_GB.UTF-8 UTF-8" >> /etc/locale.gen \
    && locale-gen en_GB.utf8 \
    && /usr/sbin/update-locale LANG=en_GB.UTF-8

# Install R CRAN
########
RUN apt-get update; apt-get install -y r-base r-base-core r-recommended \
    && gdebi -n /usr/local/rstudio.deb \
    && rm -rf /usr/local/*.deb \
    && ln -f -s /usr/lib/rstudio/bin/rstudio /usr/bin/rstudio \
    && apt-get install -fy

# Set default CRAN repo
########
RUN echo 'options(repos = c(CRAN = "https://cran.rstudio.com/"), download.file.method = "libcurl")' >> /etc/R/Rprofile.site \
    && echo 'source("/etc/R/Rprofile.site")' >> /etc/littler.r \
    && ln -s /usr/share/doc/littler/examples/install.r /usr/local/bin/install.r \
    && ln -s /usr/share/doc/littler/examples/install2.r /usr/local/bin/install2.r \
    && ln -s /usr/share/doc/littler/examples/installGithub.r /usr/local/bin/installGithub.r \
    && ln -s /usr/share/doc/littler/examples/testInstalled.r /usr/local/bin/testInstalled.r \
    && rm -rf /tmp/downloaded_packages/ /tmp/*.rds \
    && echo '"\e[5~": history-search-backward' >> /etc/inputrc \
    && echo '"\e[6~": history-search-backward' >> /etc/inputrc \
    && chmod 777 -R /usr/local/lib/R/ \
    && chmod 777 -R /usr/lib/R/ \
    && chmod 777 -R /usr/share/R/

# Install R downloaded_packages
########
COPY ./script.R /usr/local/script.R
RUN Rscript /usr/local/script.R \
    && chmod 777 -R /usr/local/lib/R/ \
    && chmod 777 -R /usr/lib/R/ \
    && chmod 777 -R /usr/share/R/
    
## Create user training
########
RUN useradd -r -s /bin/bash -U -m -d /home/training -p '' training

# Setup the user envirenment
########
ENV HOME /home/training
RUN usermod -aG sudo,audio,video training \
    && echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

WORKDIR $HOME
USER training
