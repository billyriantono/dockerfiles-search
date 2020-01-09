FROM rocker/tidyverse:3.6.0
MAINTAINER "Ed Jee" edjee96@gmail.com
USER root



RUN apt-get update \
	&& apt-get install -y --no-install-recommends apt-utils ed libnlopt-dev \
	python3 python3-pip python3-setuptools python3-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/


# Install packages
RUN install2.r --error --deps TRUE \
    furrr \
    zoo \
    ggridges \
    skimr \
    && rm -rf /tmp/downloaded_packages/ /tmp/*.rds


COPY install.R /home/rstudio/
RUN chown -R  rstudio /home/rstudio/

RUN if [ -f /home/rstudio/install.R ]; then R --quiet -f /home/rstudio/install.R; fi


# Python requirements install
COPY requirements.txt /home/rstudio/
RUN pip3 install wheel
RUN pip3 install -r home/rstudio/requirements.txt









