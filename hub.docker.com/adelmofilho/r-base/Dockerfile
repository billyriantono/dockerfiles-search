FROM ubuntu:18.04

LABEL org.label-schema.license="GPL-3.0" \
      org.label-schema.vcs-url="https://github.com/adelmofilho/Whitesnake/r-base/3.6.2" \
      org.label-schema.vendor="Hope Clouds Observation" \
      maintainer="Adelmo Filho <adelmo.aguiar.filho@gmail.com>"

# Assumir defaults nas instalações 
ENV DEBIAN_FRONTEND=noninteractive

# Instalar dependências
RUN apt-get update && apt-get install -y --no-install-recommends \
    apt-utils=1.6.12 \
    gfortran=4:7.4.0-1ubuntu2.3 \
    git=1:2.17.1-1ubuntu0.5 \
    g++=4:7.4.0-1ubuntu2.3 \
    libreadline-dev=7.0-3 \
    libx11-dev=2:1.6.4-3ubuntu0.2 \
    libxt-dev=1:1.1.5-1 \
    libpng-dev=1.6.34-1ubuntu0.18.04.2 \
    libjpeg-dev=8c-2ubuntu8 \
    libcairo2-dev=1.15.10-2ubuntu0.1 \   
    libcurl4-openssl-dev=7.58.0-2ubuntu3.8 \
    libssl-dev=1.1.1-1ubuntu2.1~18.04.5 \ 
    libxml2-dev=2.9.4+dfsg1-6.1ubuntu1.2 \
    libudunits2-dev=2.2.26-1 \
    libgdal-dev=2.2.3+dfsg-2 \
    libbz2-dev=1.0.6-8.1ubuntu0.2 \
    libzstd-dev=1.3.3+dfsg-2ubuntu1.1 \
    liblzma-dev=5.2.2-1.3 \
    locales=2.27-3ubuntu1 \
    openjdk-8-jdk=8u232-b09-0ubuntu1~18.04.1 \
    screen=4.6.2-1ubuntu1 \
    texinfo=6.5.0.dfsg.1-2 \
    texlive=2017.20180305-1 \
    texlive-fonts-extra=2017.20180305-2 \
    vim=2:8.0.1453-1ubuntu1.1 \
    wget=1.19.4-1ubuntu2.2 \
    xvfb=2:1.19.6-1ubuntu4.3 \
&& rm -rf /var/lib/apt/lists/*

# Ajuste o locale
RUN locale-gen pt_BR.UTF-8
ENV LANG pt_BR.UTF-8
ENV LANGUAGE pt_BR.UTF-8
ENV LC_ALL pt_BR.UTF-8

# Instalar R

RUN wget https://cran.rstudio.com/src/base/R-3/R-3.6.2.tar.gz && \
    tar zxvf R-3.6.2.tar.gz && \
    rm R-3.6.2.tar.gz

WORKDIR /R-3.6.2

RUN ./configure --with-cairo --with-jpeglib --enable-R-shlib --with-blas --with-lapack && \ 
    make && \
    make install

# Instalar renv
ENV RENV_VERSION 0.9.2-20
RUN R -e "install.packages('remotes', repos = c(CRAN = 'https://cloud.r-project.org'))"
RUN R -e "remotes::install_github('rstudio/renv@${RENV_VERSION}')"