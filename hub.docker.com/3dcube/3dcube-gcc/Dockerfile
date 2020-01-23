FROM gcc
VOLUME /root
env SHELL /bin/bash

RUN apt-get update && apt-get install -y locales

# Set the locale
RUN locale-gen ru_RU.UTF-8  
ENV LANG ru_RU.UTF-8  
ENV LANGUAGE ru_RU:ru:en
ENV LC_ALL ru_RU.UTF-8   

RUN apt-get install -y man

WORKDIR /root
CMD /bin/bash
