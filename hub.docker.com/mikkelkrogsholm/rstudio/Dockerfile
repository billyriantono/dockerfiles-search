FROM mikkelkrogsholm/r-base:stable

ARG RSTUDIO_VERSION
ARG PANDOC_TEMPLATES_VERSION 
ENV PANDOC_TEMPLATES_VERSION ${PANDOC_TEMPLATES_VERSION:-1.18}

## Add RStudio binaries to PATH
ENV PATH /usr/lib/rstudio-server/bin:$PATH

## Download and install RStudio server & dependencies
## Attempts to get detect latest version, otherwise falls back to version given in $VER
## Symlink pandoc, pandoc-citeproc so they are available system-wide
RUN RSTUDIO_LATEST=$(wget --no-check-certificate -qO- https://s3.amazonaws.com/rstudio-server/current.ver) \
  && [ -z "$RSTUDIO_VERSION" ] && RSTUDIO_VERSION=$RSTUDIO_LATEST || true \
  && wget -q http://download2.rstudio.org/rstudio-server-${RSTUDIO_VERSION}-amd64.deb \
  && dpkg -i rstudio-server-${RSTUDIO_VERSION}-amd64.deb \
  && rm rstudio-server-*-amd64.deb \
  ## Symlink pandoc & standard pandoc templates for use system-wide
  && ln -s /usr/lib/rstudio-server/bin/pandoc/pandoc /usr/local/bin \
  && ln -s /usr/lib/rstudio-server/bin/pandoc/pandoc-citeproc /usr/local/bin \
  && wget https://github.com/jgm/pandoc-templates/archive/${PANDOC_TEMPLATES_VERSION}.tar.gz \
  && mkdir -p /opt/pandoc/templates && tar zxf ${PANDOC_TEMPLATES_VERSION}.tar.gz \
  && cp -r pandoc-templates*/* /opt/pandoc/templates && rm -rf pandoc-templates* \
  && mkdir /root/.pandoc && ln -s /opt/pandoc/templates /root/.pandoc/templates \
  && rm ${PANDOC_TEMPLATES_VERSION}.tar.gz \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/ \
  ## RStudio wants an /etc/R, will populate from $R_HOME/etc
  && mkdir -p /etc/R \
  ## Write config files in $R_HOME/etc
  && echo '\n\
    \n# Configure httr to perform out-of-band authentication if HTTR_LOCALHOST \
    \n# is not set since a redirect to localhost may not work depending upon \
    \n# where this Docker container is running. \
    \nif(is.na(Sys.getenv("HTTR_LOCALHOST", unset=NA))) { \
    \n  options(httr_oob_default = TRUE) \
    \n}' >> /usr/local/lib/R/etc/Rprofile.site \
  && echo "PATH=\"${PATH}\"" >> /usr/local/lib/R/etc/Renviron \
  ## Need to configure non-root user for RStudio
  && useradd rstudio \
  && echo "rstudio:rstudio" | chpasswd \
	&& mkdir /home/rstudio \
	&& chown rstudio:rstudio /home/rstudio \
	&& addgroup rstudio staff \
  ## configure git not to request password each time 
  && git config --system credential.helper 'cache --timeout=3600' \
  && git config --system push.default simple \
  ## Set up S6 init system
  && wget -P /tmp/ https://github.com/just-containers/s6-overlay/releases/download/v1.11.0.1/s6-overlay-amd64.tar.gz \
  && tar xzf /tmp/s6-overlay-amd64.tar.gz -C / \
  && mkdir -p /etc/services.d/rstudio \
  && echo '#!/bin/bash \
           \n exec /usr/lib/rstudio-server/bin/rserver --server-daemonize 0' \
           > /etc/services.d/rstudio/run \
   && echo '#!/bin/bash \
           \n rstudio-server stop' \
           > /etc/services.d/rstudio/finish

COPY userconf.sh /etc/cont-init.d/userconf

EXPOSE 8787

CMD ["/init"]
