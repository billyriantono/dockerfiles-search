FROM scratch
ADD centos-7.4.1708-docker.tar.xz /

LABEL name="CentOS Base Image" \
    vendor="CentOS" \
    license="GPLv2" \
    build-date="20170911"

ADD ffmpeg.tar.gz /bin
CMD chown root:root /bin

CMD ["/bin/ffmpeg"]
