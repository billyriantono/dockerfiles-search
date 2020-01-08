FROM wernight/phantomjs:latest
USER root
# Install japanese font 
RUN set -x \ 
 && apt-get update \
 && apt-get install -y fontconfig \
        fonts-ipafont-gothic \
 && fc-cache -fv \
 && apt-get clean \
 && rm -rf /tmp/* /var/lib/apt/lists/*

CMD ["phantomjs"]