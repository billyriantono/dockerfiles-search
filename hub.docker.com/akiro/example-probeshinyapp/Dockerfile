# build command: docker build -t probe-shiny-app .

FROM akiro/r-base:R-3.4.4

MAINTAINER Andrea Melloncelli "andrea.melloncelli@gmail.com"

# system libraries of general use
RUN apt-get update && apt-get install -y \
sudo \
pandoc \
pandoc-citeproc \
libcairo2-dev \
libxt-dev \
libssl-dev \
libssh2-1-dev \
libssl1.0.0 \
libxml2 \
libcurl4-openssl-dev \
libssl-dev \
libxml2-dev

# system library dependency for the milano app
RUN apt-get update && apt-get install -y \
libmpfr-dev

# basic shiny functionality
# RUN R -e "install.packages(c('shiny', 'rmarkdown'), repos='https://cloud.r-project.org/')"

# install dependencies of this app
RUN R -e "install.packages('devtools', repos='https://cloud.r-project.org/')"
RUN R -e "install.packages('packrat', repos='https://cloud.r-project.org/')"

################
# copy the app to the image

# copy and set up packrat
#RUN mkdir /root/appPackage
ENV file packrat/init.R
COPY $file /root/appPackage/$file
ENV file packrat/packrat.lock
COPY packrat/packrat.lock /root/appPackage/packrat/packrat.lock
ENV file packrat/packrat.opts

COPY $file /root/appPackage/$file
RUN R -e 'setwd("/root/appPackage"); packrat::on(); packrat::restore();' 
RUN cp -r /root/appPackage/packrat/lib/x86_64-pc-linux-gnu/$R_BASE_VERSION/ /usr/local/lib/R/site-library/

# copy and install the package
COPY DESCRIPTION NAMESPACE probeShinyApp.Rproj /root/appPackage/
ENV dir inst
COPY $dir /root/appPackage/$dir
ENV dir R
COPY $dir /root/appPackage/$dir
RUN R -e 'setwd("/root/appPackage"); library(devtools); build(); install()'


RUN R CMD INSTALL /root/appPackage/.
RUN rm -rf /root/appPackage

COPY inst/app-container/Rprofile.site /usr/lib/R/etc/

RUN R --version

EXPOSE 3838

CMD ["R", "-e probeShinyApp::launch_shiny_app()"]
