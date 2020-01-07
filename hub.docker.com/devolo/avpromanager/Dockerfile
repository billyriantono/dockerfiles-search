FROM ubuntu:16.04

ENV INSTALL_DEB avpromanager_6.10.0-0_amd64.deb

RUN DEBIAN_FRONTEND=noninteractive apt update \
  && apt -y install wget gdebi \
  && wget https://www.devolo.de/fileadmin/user_upload/Business_Solution/Download/Software_pro/dLAN_R__AVpro_manager/${INSTALL_DEB} \
  && gdebi --non-interactive ${INSTALL_DEB}

CMD ["avpromanager.bin"]
