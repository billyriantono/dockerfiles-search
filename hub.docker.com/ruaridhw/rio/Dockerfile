FROM ruaridhw/r-pkgdev:latest
LABEL org.label-schema.license="GPL-2.0" \
      org.label-schema.vcs-url="https://github.com/ruaridhw/dockerfiles/tree/master/rio" \
      org.label-schema.vendor="" \
      maintainer="Ruaridh Williamson <ruaridh.williamson@gmail.com>"

ENV workingdir /usr/local/R

ADD https://api.github.com/repos/ruaridhw/rio/compare/master...HEAD /dev/null
RUN git clone https://github.com/ruaridhw/rio "$workingdir"

WORKDIR "$workingdir"

RUN Rscript -e 'devtools::install_dev_deps()'

RUN rm -rf /usr/local/R

CMD ["R"]
