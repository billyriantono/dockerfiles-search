FROM debian:latest

MAINTAINER "Babak Naimi" naimi.b@gmail.com

ENV LC_ALL=en_US.UTF-8 \
    LANG=en_US.UTF-8 \
    TERM=xterm

RUN apt-get update \
  && apt-get install -y --no-install-recommends libxml2-dev libssl-dev libcurl4-openssl-dev libv8-3.14-dev \
  binutils libproj-dev lbzip2 libfftw3-dev libgdal-dev \
    libgeos-dev libgsl0-dev libgl1-mesa-dev libglu1-mesa-dev \
    libhdf4-alt-dev libhdf5-dev libjq-dev liblwgeom-dev libpq-dev \
    libprotobuf-dev libnetcdf-dev libsqlite3-dev libudunits2-dev \
    netcdf-bin postgis protobuf-compiler sqlite3 tk-dev unixodbc-dev \
    bash-completion ca-certificates ccache file fonts-texgyre g++ \
    gfortran gsfonts libblas-dev libbz2-1.0 libcurl3 libicu57 \
    libjpeg62-turbo libopenblas-dev libpangocairo-1.0-0 libpcre3 \
    libpng16-16 libreadline7 libtiff5 liblzma5 locales make \
    unzip zip zlib1g libpng-dev sudo gdebi-core pandoc \
    pandoc-citeproc libcairo2-dev libxt-dev libbz2-dev \
    xtail wget subversion tcl8.6-dev tk8.6-dev texinfo libtiff5-dev \
    texlive-extra-utils texlive-fonts-recommended libreadline-dev \
    texlive-fonts-extra texlive-latex-recommended default-jdk \ 
    curl perl rsync libicu-dev libpcre3-dev libjpeg-dev \
    libpango1.0-dev liblzma-dev libx11-dev libxt-dev \
    x11proto-core-dev xauth xfonts-base xvfb zlib1g-dev \
  && rm -rf /var/lib/apt/lists/* \
  && echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen \
  && locale-gen en_US.utf8 \
  && /usr/sbin/update-locale LANG=en_US.UTF-8


########################
 # Install R from source (source: Dockerfile rocker/r-ver, 05/05/2019)

ENV R_BASE_VERSION R-3-6-0

 RUN cd tmp/ \
  ## Download source code
  && svn co https://svn.r-project.org/R/tags/${R_BASE_VERSION}/ \
  ## Extract source code \
  && cd ${R_BASE_VERSION} \
  ## Get source code of recommended packages \
  && ./tools/rsync-recommended \
  ## Set compiler flags \
  && R_PAPERSIZE=letter \
    R_BATCHSAVE="--no-save --no-restore" \
    R_BROWSER=xdg-open \
    PAGER=/usr/bin/pager \
    PERL=/usr/bin/perl \
    R_UNZIPCMD=/usr/bin/unzip \
    R_ZIPCMD=/usr/bin/zip \
    R_PRINTCMD=/usr/bin/lpr \
    LIBnn=lib \
    AWK=/usr/bin/awk \
    CFLAGS="-g -O2 -fstack-protector-strong -Wformat -Werror=format-security -Wdate-time -D_FORTIFY_SOURCE=2 -g" \
    CXXFLAGS="-g -O2 -fstack-protector-strong -Wformat -Werror=format-security -Wdate-time -D_FORTIFY_SOURCE=2 -g" \
  ## Configure options \
  ./configure --enable-R-shlib \
               --enable-memory-profiling \
               --with-readline \
               --with-blas \
               --with-tcltk \
               --disable-nls \
               --with-recommended-packages \
  ## Build and install \
  && make \
  && make install \
  ## Add a default CRAN mirror \
  && echo "options(repos = c(CRAN = 'https://cran.rstudio.com/'), download.file.method = 'libcurl')" >> /usr/local/lib/R/etc/Rprofile.site \
  ## Add a library directory (for user-installed packages) \
  && mkdir -p /usr/local/lib/R/site-library \
  && chown root:staff /usr/local/lib/R/site-library \
  && chmod g+wx /usr/local/lib/R/site-library \
  ## Fix library path \
  && echo "R_LIBS_USER='/usr/local/lib/R/site-library'" >> /usr/local/lib/R/etc/Renviron \
  && echo "R_LIBS=\${R_LIBS-'/usr/local/lib/R/site-library:/usr/local/lib/R/library:/usr/lib/R/library'}" >> /usr/local/lib/R/etc/Renviron \
  ## install packages from CRAN.rsudio repo \
  && CRAN=http://cran.rstudio.com \
  && echo CRAN=$CRAN >> /etc/environment \
  && export CRAN=$CRAN \
  ## CRAN becomes default only in versioned images \
  ## Use littler installation scripts \
  && Rscript -e "install.packages(c('littler', 'docopt'), repo = '$CRAN')" \
  && ln -s /usr/local/lib/R/site-library/littler/examples/install2.r /usr/local/bin/install2.r \
  && ln -s /usr/local/lib/R/site-library/littler/examples/installGithub.r /usr/local/bin/installGithub.r \
  && ln -s /usr/local/lib/R/site-library/littler/bin/r /usr/local/bin/r \
  ## TEMPORARY WORKAROUND to get more robust error handling for install2.r prior to littler update \
  && curl -O /usr/local/bin/install2.r https://github.com/eddelbuettel/littler/raw/master/inst/examples/install2.r \
  && Rscript -e "install.packages(c('shiny', 'shinydashboard','V8' , 'Rcpp'), repo = '$CRAN')" \
  && chmod +x /usr/local/bin/install2.r \
  ## Clean up from R source install \
  && cd / \
  && rm -rf /tmp/* \
  && apt-get remove --purge -y $BUILDDEPS \
  && apt-get autoremove -y \
  && apt-get autoclean -y \
  && rm -rf /var/lib/apt/lists/*

COPY ./DockerConfig/requirements.R /tmp/requirements.R 

RUN Rscript /tmp/requirements.R

RUN wget --no-verbose https://download3.rstudio.org/ubuntu-14.04/x86_64/VERSION -O "version.txt" && \
    VERSION=$(cat version.txt)  && \
    wget --no-verbose "https://download3.rstudio.org/ubuntu-14.04/x86_64/shiny-server-$VERSION-amd64.deb" -O ss-latest.deb && \
    gdebi -n ss-latest.deb && \
    rm -f version.txt ss-latest.deb && \
    . /etc/environment && \
    cp -R /usr/local/lib/R/site-library/shiny/examples/* /srv/shiny-server/

EXPOSE 3838


# Copy configuration files into the Docker image
COPY shiny-server.conf  /etc/shiny-server/shiny-server.conf

COPY shiny-server.sh /usr/bin/shiny-server.sh

RUN chmod -R 755 /srv/shiny-server/ \
  && chmod -R 755 /usr/bin/shiny-server.sh

COPY ./DockerConfig/Additional_packages.R /tmp/Additional_packages.R

RUN Rscript /tmp/Additional_packages.R

CMD ["/usr/bin/shiny-server.sh"]