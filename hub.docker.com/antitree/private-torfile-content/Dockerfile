FROM debian:stretch-slim

LABEL maintainer "Anthony Mastrean <anthony.mastrean@gmail.com>"

WORKDIR /root

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        imagemagick \
        wget \
    && wget -q http://www.fmwconcepts.com/imagemagick/script_list.txt \
    && egrep -o '^\w+' script_list.txt > script_names.txt \
    && xargs -a script_names.txt -t -I"{}" wget -q -O "{}" "http://www.fmwconcepts.com/imagemagick/downloadcounter.php?scriptname={}&dirname={}" \
    && chmod +x * \
    && savedPackages="imagemagick" \
    && apt-mark auto '.*' > /dev/null \
    && apt-mark manual $savedPackages \
    && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false \
    && rm -fr *.txt /var/cache/apt/* /var/lib/apt/lists/*

ENTRYPOINT ["/bin/sh", "-c"]
CMD ["ls -1"]
