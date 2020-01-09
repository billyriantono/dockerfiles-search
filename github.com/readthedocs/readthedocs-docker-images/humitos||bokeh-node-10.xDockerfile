# Read the Docs - Bokeh custom image with NodeJS 10.x
FROM readthedocs/build:latest
LABEL mantainer="Read the Docs <support@readthedocs.com>"
LABEL version="bokeh-nodejs-10.x"

USER root

# https://github.com/nodesource/distributions/blob/master/README.md#debinstall
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get install -y nodejs

USER docs
WORKDIR /

CMD ["/bin/bash"]
