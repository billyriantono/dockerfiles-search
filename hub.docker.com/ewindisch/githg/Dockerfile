FROM debian
RUN apt-get update; \
    apt-get install -qy mercurial git

# Remove setuid binaries
find / -perm +6000 -type f -exec rm {} \;
