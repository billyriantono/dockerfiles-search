FROM hackyo/debian
MAINTAINER hackyo <137120918@qq.com>
ADD https://codeload.github.com/git/git/tar.gz/v2.11.0 /git/git-2.11.0.tar.gz
RUN apt-get install -y make perl tk libcurl4-gnutls-dev libexpat1-dev gettext libz-dev libssl-dev gcc && apt-get clean && apt-get autoremove \
    && cd /git \
    && tar xzf git-2.11.0.tar.gz && cd git-2.11.0 \
    && make prefix=/usr/local all \
    && make prefix=/usr/local install \
    && cd / \
    && rm -rf git \
    && git --version
CMD ["bash"]
