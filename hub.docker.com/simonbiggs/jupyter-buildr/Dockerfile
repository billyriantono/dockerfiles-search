FROM simonbiggs/jupyter-buildjulia

MAINTAINER Simon Biggs <mail@simonbiggs.net>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get -y upgrade

# R installation
RUN apt-get install -y r-base r-base-dev r-cran-rcurl libreadline-dev
RUN echo 'options(repos=structure(c(CRAN="http://cran.rstudio.com")))' > ~/.Rprofile
RUN mkdir -p ~/.R; echo "PKG_CXXFLAGS = '-std=c++11'" > ~/.R/Makevars
RUN echo "install.packages(c('ggplot2', 'XML', 'plyr', 'randomForest', 'Hmisc', 'stringr', 'RColorBrewer', 'reshape', 'reshape2'))" | R --no-save
RUN echo "install.packages(c('RCurl', 'devtools', 'dplyr'))" | R --no-save
RUN echo "library(devtools); install_github('armstrtw/rzmq'); install_github('takluyver/IRdisplay'); install_github('takluyver/IRkernel'); IRkernel::installspec()" | R --no-save
