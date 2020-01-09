FROM debian:8

LABEL MAINTAINER="Cédric DELPAS <cedric.delpas@gmail.com>

EXPOSE 80 443

RUN echo "deb http://packages.openmediavault.org/public erasmus main" | tee -a /etc/apt/sources.list.d/openmediavault.list \
    && echo "deb http://packages.omv-extras.org/debian/ erasmus main" | sudo tee -a /etc/apt/sources.list.d/omv-extras-org-kralizec.list \
    && wget -O - http://packages.openmediavault.org/public/archive.key | apt-key add - \
    && apt-get update \
    && apt-get install openmediavault-keyring postfix -y --force-yes \
    && apt-get install php-apc openmediavault openmediavault-omvextrasorg -y --force-yes
    
    
CMD [ "omv-initsystem" ]

ENTRYPOINT ["nginx" ]
