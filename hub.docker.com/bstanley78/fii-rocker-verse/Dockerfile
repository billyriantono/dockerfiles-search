FROM rocker/verse

LABEL maintainer="analytics@fii.org"

RUN sudo R -e "install.packages(c('riverplot','yaml','splitstackshape','RJSONIO','plotly','hash','ggridges','aws.s3','assertr','zipcode', 'zoo', 'plyr', 'httr', 'base64enc', 'rjson', 'rlang'), dependencies=TRUE)"
RUN sudo R -e "install.packages(c('DT'), dependencies=TRUE)"

RUN sudo apt-get -qq update && \
    sudo apt-get -y install git ssh curl python-setuptools && \
    sudo easy_install pip && \
    sudo easy_install awscli
