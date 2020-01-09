FROM opensuse:42.3

LABEL maintainer="karl@rstudio.com"

EXPOSE 8788/tcp

# update repos
RUN set -x \
    && zypper --non-interactive update -y

RUN zypper --non-interactive install -y \
    wget \
    tar \
    libuser-devel

# overwrite libuser.conf to disable group shadowing as /etc/gshadow is not available in the docker container
ADD libuser.conf /etc/libuser.conf

# install RStudio Server Pro session bits
ARG RSTUDIO_DOWNLOAD_URL=https://www.rstudio.org/download/latest/stable
RUN wget \
    ${RSTUDIO_DOWNLOAD_URL}/session/suse12_64/rsp-session-opensuse-latest.tar.gz
RUN mkdir -p /usr/lib/rstudio-server
RUN tar -zxvf ./rsp-session-opensuse-latest.tar.gz -C /usr/lib/rstudio-server/
RUN mv /usr/lib/rstudio-server/rsp-session*/* /usr/lib/rstudio-server/
RUN rm -rf /usr/lib/rstudio-server/rsp-session*

# clean up zip
RUN rm -f ./rsp-session-opensuse-latest.tar.gz
