FROM scratch
ADD alpine-minirootfs-3.10.2-x86_64.tar.gz /
RUN sed -i 's/http:\/\/dl-cdn.alpinelinux.org\/alpine\/v3.10\/main/http:\/\/mirror1.hs-esslingen.de\/pub\/Mirrors\/alpine\/v3.10\/main/g' /etc/apk/repositories && \
    sed -i 's/http:\/\/dl-cdn.alpinelinux.org\/alpine\/v3.10\/community/http:\/\/mirror1.hs-esslingen.de\/pub\/Mirrors\/alpine\/v3.10\/community/g' /etc/apk/repositories
CMD ["/bin/sh"]
