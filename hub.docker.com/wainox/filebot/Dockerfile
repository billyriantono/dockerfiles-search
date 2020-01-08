FROM rednoah/filebot

RUN apt-get update \
	&& \
	apt-get install -y unrar-free \
	&& \
    apt-get clean \
    && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

