## Forked FROM statwonk/r-base-dev
FROM ubuntu:16.04
MAINTAINER Can Altıparmak <can6parmak@gmail.com>

## Set a default user. Available via runtime flag `--user docker`
## Add user to 'staff' group, granting them write privileges to /usr/local/lib/R/site.library
## User should also have & own a home directory (for rstudio or linked volumes to work properly).
RUN useradd docker \
	&& mkdir /home/docker \
	&& chown docker:docker /home/docker \
	&& addgroup docker staff \
    && echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen \
	&& locale-gen en_US.utf8 \
	&& /usr/sbin/update-locale LANG=en_US.UTF-8

ENV LC_ALL en_US.UTF-8
ENV LANG en_US.UTF-8

## Set a default CRAN repo
RUN echo 'deb http://cran.rstudio.com/bin/linux/ubuntu xenial/' >> /etc/apt/sources.list \
        && apt-get update \
	&& apt-get install -y --force-yes --no-install-recommends \
		r-base-dev wget curl git \
        && echo 'options(repos = list(CRAN = "http://cran.rstudio.com/"))' >> /etc/R/Rprofile.site \
    && apt-get clean \
	&& rm -rf /var/lib/apt/lists/* /tmp/* \
        /usr/share/man/* /usr/share/groff/* /usr/share/info/* \
        /usr/share/lintian/* /usr/share/linda/* /var/cache/man/*

CMD ["R"]

