FROM alpine:3.5

MAINTAINER vici <heyuhuade@gmail.com>

COPY ./IntelliJIDEALicenseServer_linux_amd64 /

RUN chmod a+x \
        /IntelliJIDEALicenseServer_linux_amd64

EXPOSE 20701

CMD ["-u","kingsoft"]

ENTRYPOINT ["/IntelliJIDEALicenseServer_linux_amd64","-p","20701"]

