# obgr/D-CasperJS - Debian 9 & PhantomJS based CasperJS image.

FROM debian:9
MAINTAINER https://github.com/obgr

############################
#   Install Dependencies   #
############################

RUN apt-get update \
 && apt-get install -y --no-install-recommends \
                    bzip2 \
                    ca-certificates \
                    curl \
                    dumb-init \
                    git \
                    libfontconfig \
                    python \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

############################
#  Environment Variables   #
############################

#ENV DEBIAN_FRONTEND noninteractive
ENV PHJS_VER 2.1.1
ENV PHJS_PKG phantomjs-${PHJS_VER}-linux-x86_64.tar.bz2
ENV PHJS_UN phantomjs
ENV PHJS_UID 991
ENV PHJS_GID 991

############################
#    Install PhantomJS     #
############################

# Add PhantomJS Service Account and group
RUN groupadd -r ${PHJS_UN} -g ${PHJS_GID} \
 && useradd -r -s /bin/bash -M -c "PhantomJS Service Account" -u ${PHJS_UID} -g ${PHJS_UN} ${PHJS_UN}

RUN set -x  \
    # Install official PhantomJS release
 && mkdir /tmp/phantomjs \
 && curl -L https://bitbucket.org/ariya/phantomjs/downloads/${PHJS_PKG} \
        | tar -xj --strip-components=1 -C /tmp/phantomjs \
 && mv /tmp/phantomjs/bin/phantomjs /usr/local/bin \
 && rm -rf /tmp/phantomjs \
    # Test Run PhantomJS
 && su ${PHJS_UN} -s /bin/sh -c "phantomjs --version"

############################
#     Install CasperJS     #
############################

RUN cd /opt \
 && git clone https://github.com/casperjs/casperjs.git \
 && cd casperjs \
    # Cleanup
 && rm -rf ./.git \
 && rm -rf *.gemspec docs rpm samples \
    # Create symbolic link
 && ln -sf `pwd`/bin/casperjs /usr/local/bin/casperjs \
    # Test run CasperJS
 && su ${PHJS_UN} -s /bin/sh -c "casperjs" 

############################
#  Purge excess packages   #
############################

RUN apt-get purge -y --auto-remove \
                    bzip2 \
                    curl \
                    git \
 && apt-get clean

############################
#         Startup          #
############################

USER ${PHJS_UN}

ENTRYPOINT ["/usr/bin/dumb-init", "--"]

CMD ["/bin/bash"]
