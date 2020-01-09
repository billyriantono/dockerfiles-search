FROM openjdk:8-jdk

RUN apt-get update \
  && apt-get -y install sudo \
  && adduser --disabled-password --gecos '' tizen \
  && adduser tizen sudo \
  && echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

WORKDIR /home/tizen/workdir

RUN chown -R tizen:tizen /home/tizen

USER tizen

RUN curl http://download.tizen.org/sdk/Installer/tizen-studio_3.3/web-cli_Tizen_Studio_3.3_ubuntu-64.bin -o ../tizen.bin

RUN mkdir -p /home/tizen/tizen-studio \
 && chmod +x ../tizen.bin \
 && ./../tizen.bin --accept-license /home/tizen/tizen-studio \
 && rm ../tizen.bin \
 && chown -R tizen:tizen /home/tizen/workdir

ENV PATH="/home/tizen/tizen-studio/tools/ide/bin:${PATH}"
