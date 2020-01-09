# mauck Dockerfile

# Create an image to build RPMs a-là mock

FROM fedora:28
LABEL maintainer="jaybeeunix@gmail.com"
LABEL version="0.1"
ENV MAUCK_RESULTS="/results" \
    MAUCK_WORKING="/working" \
    MAUCK_USER="mauckuser"
RUN mkdir "${MAUCK_RESULTS}" "${MAUCK_WORKING}" && \
    dnf --assumeyes install @buildsys-build "dnf-command(builddep)" && \
    useradd -r "${MAUCK_USER}" -U -m && \
    chown "${MAUCK_USER}" "${MAUCK_RESULTS}" "${MAUCK_WORKING}"
WORKDIR $MAUCK_WORKING
COPY ["./mauck", "/"]
ENTRYPOINT ["/mauck"]
