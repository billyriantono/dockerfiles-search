FROM debian:stretch-slim

RUN apt-get update && apt-get install -y \
    libgl1-mesa-dev \
    libx11-dev \
    libxext6 \
    lsb-core 

ENV PATH="/usr/local/bin:${PATH}"

ADD REDline_Build_51.47289_Installer.sh /data/
RUN ./data/REDline_Build_51.47289_Installer.sh

ENTRYPOINT ["/usr/local/bin/REDline"]
CMD ["--help"]
