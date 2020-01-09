# ---------------------------------------------
#
# Dockerfile best practices
# Refer: http://docs.docker.com/engine/articles/dockerfile_best-practices/
#
# This file makes use of contributions from Rafal Szkup, Application Engineer, UoA
# and the iNZight Team, UoA
#
# ---------------------------------------------


FROM r-base:3.6.1

COPY shiny-server.sh /opt/

RUN apt-get update \
    && apt-get install -y -q \
        libssl-dev \
 #      libssl1.0.0 \
        gnupg2 \
        libxml2-dev \
        libcairo2-dev \
        libxt-dev \
        libcurl4-openssl-dev \
        sudo \
        wget \
        gdebi-core \
        default-jre \
        default-jdk \
        xtail \
        pandoc \
    pandoc-citeproc \
        
        
    && wget --no-verbose -O libssl.deb https://mirrors.mediatemple.net/debian-archive/debian/pool/main/o/openssl/libssl0.9.8_0.9.8o-4squeeze14_amd64.deb \
    && dpkg -i libssl.deb \
    && rm -f libssl.deb \
    && sudo R CMD javareconf \
    && apt-get install -y -q r-cran-rjava \
    && apt-get install -y -q libgdal-dev libproj-dev \
    && R -e "install.packages('rmarkdown', dependencies = TRUE, repos='http://cran.rstudio.com/', lib='/usr/lib/R/site-library')" \
    && R -e "install.packages('shiny', dependencies = TRUE, repos='http://cran.rstudio.com/', lib='/usr/lib/R/site-library')" \
    && R -e "install.packages('DT', dependencies = TRUE, repos='http://cran.rstudio.com/', lib='/usr/lib/R/site-library')" \
# expose ports
    && wget --no-verbose -O shiny-server.deb https://download3.rstudio.org/ubuntu-14.04/x86_64/shiny-server-1.5.12.933-amd64.deb \
    && dpkg -i shiny-server.deb \
    && chmod +x /opt/shiny-server.sh \
    && rm -f shiny-server.deb \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


# expose ports
EXPOSE 3838

# we do NOT initiate any process - treat this image as abstract class equivalent

