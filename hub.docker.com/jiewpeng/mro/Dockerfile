FROM ubuntu:16.04

ENV MRO_VERSION_MAJOR 3
ENV MRO_VERSION_MINOR 4
ENV MRO_VERSION_BUGFIX 1
ENV MRO_VERSION $MRO_VERSION_MAJOR.$MRO_VERSION_MINOR.$MRO_VERSION_BUGFIX

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    wget \
    ca-certificates \
    # build-essential for installing packages
    build-essential \
    # cairo and libxt are dependencies for cairo, a dependency of shiny
    libcairo2-dev libxt-dev &&\
    # install MRO
    wget https://mran.blob.core.windows.net/install/mro/$MRO_VERSION/microsoft-r-open-$MRO_VERSION.tar.gz &&\
    tar -xzf microsoft-r-open-$MRO_VERSION.tar.gz &&\
    ./microsoft-r-open/install.sh -a -u &&\
    rm -r microsoft-r-open && rm microsoft-r-open-$MRO_VERSION.tar.gz &&\
    # link full path of MRO to /usr/lib/R
    ln -s /opt/microsoft/ropen/$MRO_VERSION/lib64/R /usr/lib/R &&\
    # Overwrite default behaviour to never save workspace, blatantly copied from nuest/docker-mro
    echo 'utils::assignInNamespace("q", function(save = "no", status = 0, runLast = TRUE) { \
     .Internal(quit(save, status, runLast)) }, "base")' >> /usr/lib/R/etc/Rprofile.site &&\
    echo 'utils::assignInNamespace("quit", function(save = "no", status = 0, runLast = TRUE) { \
     .Internal(quit(save, status, runLast)) }, "base")' >> /usr/lib/R/etc/Rprofile.site

# fix C++11 standard requested but CXX11 is not defined issue
ADD https://raw.githubusercontent.com/bi-sdal/mro-ldap-ssh-c7/master/Makeconf  /usr/lib/R/etc/Makeconf

RUN \
    # install shiny
    Rscript -e "install.packages('shiny', dependencies = TRUE)" &&\
    Rscript -e "install.packages('shinythemes', dependencies = TRUE)" &&\
    Rscript -e "install.packages('shinyBS', dependencies = TRUE)" &&\
    # minimise image size
    rm -rf /var/lib/apt/lists/*

CMD ["/usr/bin/R"]
