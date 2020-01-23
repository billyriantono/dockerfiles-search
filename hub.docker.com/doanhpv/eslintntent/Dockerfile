FROM alpine 
LABEL maintainer "David Sn <divad.nnamtdeis@gmail.com>"

# Install perl with perl-archive-zip for crc32 checksums
RUN apk --no-cache add \
        perl \
        perl-archive-zip \
    && rm -rf /var/cache/apk/*

# Copy extract script
COPY splitupdate /bin/
RUN chmod +x /bin/splitupdate

# Work in the data directory, mounted files are expected to be here
WORKDIR /data

# That's where the magic starts~
ENTRYPOINT ["splitupdate", "UPDATE.APP"]