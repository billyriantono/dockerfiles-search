FROM centos:centos7
LABEL maintainer  "af139784"

RUN yum -y install epel-release
RUN yum update -y
RUN yum upgrade -y
RUN yum clean all -y
# RUN yum reinstall -y glibc-common
RUN yum install -y locales java-1.8.0-openjdk-devel tar wget

# R devtools pre-requisites:
RUN wget -P /etc/yum.repos.d/ https://copr.fedorainfracloud.org/coprs/petersen/pandoc/repo/epel-7/petersen-pandoc-epel-7.repo
RUN yum install -y pandoc pandoc-citeproc
#RUN yum install -y git xml2 libxml2-devel curl curl-devel openssl-devel pandoc
RUN yum install -y git xml2 libxml2-devel curl curl-devel openssl-devel 
# Plotly needs libcurl
RUN yum install libcurl-devel -y

WORKDIR /home/root
RUN yum install -y R

RUN R -e "install.packages(c('shiny', 'rmarkdown', 'devtools', 'RJDBC', 'tidyverse', 'plotly', 'RPostgreSQL', 'lubridate', 'DT', 'shinythemes', 'igraph', 'visNetwork', 'linkcomm', 'data.table', 'shinydashboard', 'shinyjs', 'RSelenium', 'flexdashboard', 'RJSONIO', 'Hmisc', 'crosstalk', 'shinycssloaders', 'forecast', 'tidymodels'), repos='https://cran.r-project.org')"

#-----------------------

# Add RStudio binaries to PATH
# export PATH="/usr/lib/rstudio-server/bin/:$PATH"
ENV PATH /usr/lib/rstudio-server/bin/:$PATH 
ENV LANG en_US.UTF-8

#RUN yum install -y openssl098e supervisor passwd pandoc
RUN yum install -y openssl-devel supervisor passwd pandoc

# Install Rstudio server:
RUN wget https://download2.rstudio.org/rstudio-server-rhel-1.1.463-x86_64.rpm
RUN yum -y install --nogpgcheck rstudio-server-rhel-1.1.463-x86_64.rpm \
	&& rm -rf rstudio-server-rhel-1.1.463-x86_64.rpm

RUN groupadd rstudio \
	&& useradd -g rstudio rstudio \
	&& echo rstudio | passwd rstudio --stdin

# Install Shiny server:
#RUN wget https://download3.rstudio.org/centos5.9/x86_64/shiny-server-1.5.7.888-rh5-x86_64.rpm
#RUN yum -y install --nogpgcheck shiny-server-1.5.7.888-rh5-x86_64.rpm \
#	&& rm -rf shiny-server-1.5.7.888-rh5-x86_64.rpm
RUN wget https://download3.rstudio.org/centos6.3/x86_64/shiny-server-1.5.9.923-x86_64.rpm
RUN yum -y install --nogpgcheck shiny-server-1.5.9.923-x86_64.rpm \
	&& rm -rf shiny-server-1.5.9.923-x86_64.rpm

RUN mkdir -p /var/log/shiny-server \
	&& chown shiny:shiny /var/log/shiny-server \
	&& chown shiny:shiny -R /srv/shiny-server \
	&& chmod 755 -R /srv/shiny-server \
	&& chown shiny:shiny -R /opt/shiny-server/samples/sample-apps \
	&& chmod 755 -R /opt/shiny-server/samples/sample-apps 

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
RUN mkdir -p /var/log/supervisor \
	&& chmod 755 -R /var/log/supervisor


EXPOSE 8787 3838


CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"] 

