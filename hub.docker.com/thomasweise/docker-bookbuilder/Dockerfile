#
# thomasweise/docker-bookbuilder
#
# This is an image with a basic TeX Live installation,
# pandoc, and R, and my bookbuildeR R package.
# Source: https://github.com/thomasWeise/docker-bookbuilder/
# License: GNU GENERAL PUBLIC LICENSE, Version 3, 29 June 2007
# The license applies to the way the image is built, while the
# software components inside the image are under the respective
# licenses chosen by their respective copyright holders.
#
FROM thomasweise/docker-pandoc-r
MAINTAINER Thomas Weise <tweise@hfuu.edu.cn>

# do all the installation
RUN apt-get clean &&\
    apt-get update &&\
    apt-get autoclean -y &&\
    apt-get autoremove -y &&\
    apt-get update &&\
# install git, which we need to access code repositories
    apt-get install -f -y git &&\
    cd /tmp/ &&\
    Rscript -e "if(!(require(\"bookbuildeR\"))) devtools::install_github(\"thomasWeise/bookbuildeR\")" &&\
    Rscript -e "if(!(require(\"bookbuildeR\"))) { q(status=1L); }" &&\
# downloading some csl files
    curl -L --output "$PANDOC_DIR/association-for-computing-machinery.csl" http://www.zotero.org/styles/association-for-computing-machinery &&\
# the directories for input and output
    mkdir /input/ &&\
    mkdir /output/ &&\
# cleanup
    apt-get clean &&\
    apt-get autoclean -y &&\
    apt-get autoremove -y &&\
    apt-get clean &&\
    rm -rf /tmp/* /var/tmp/* &&\
    rm -rf /var/lib/apt/lists/* &&\
    rm -f /etc/ssh/ssh_host_*

ADD scripts /bin/

ENTRYPOINT ["/bin/main.sh"]

# the volumes for the input and output
VOLUME ["/input/", "/output/"]
