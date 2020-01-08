FROM hadoopware/hexo

MAINTAINER Andrey <andreyk@hadoopware.io>


#################### BEGIN INSTALLATION #############################
RUN groupadd -r hadoopware && useradd -r -g hadoopware hadoopware 
ENV INSTALL_HOME="/opt/hadoopware.io"
#################### INSTALLATION END #############################


#################### Start Hexo ################################
ENV HW_REPOSITORY_URL="https://github.com/hadoopware/hadoopware.io.git"
RUN git clone $HW_REPOSITORY_URL $INSTALL_HOME

## Run ##
CMD ["/opt/hadoopware.io/bin/start.sh"]


