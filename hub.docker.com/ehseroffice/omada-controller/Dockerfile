FROM ubuntu:18.04
MAINTAINER Christoph Eßer <christoph@cehser.de>

# install runtime dependencies
RUN apt-get update &&\
  apt-get install -y libcap-dev net-tools wget unzip &&\
  rm -rf /var/lib/apt/lists/*

# install omada controller (instructions taken from install.sh); then create a user & group and set the appropriate file system permissions
RUN cd /tmp &&\
  wget https://static.tp-link.com/2019/201903/20190326/Omada_Controller_v3.1.4_linux_x64.tar.gz.zip &&\
  unzip Omada_Controller_v3.1.4_linux_x64.tar.gz.zip &&\
  tar zxvf Omada_Controller_v3.1.4_linux_x64.tar.gz &&\
  cd Omada_Controller_v3.1.4_linux_x64最初 &&\
  mkdir /opt/tplink/EAPController -vp &&\
  cp bin /opt/tplink/EAPController -r &&\
  cp data /opt/tplink/EAPController -r &&\
  cp properties /opt/tplink/EAPController -r &&\
  cp webapps /opt/tplink/EAPController -r &&\
  cp keystore /opt/tplink/EAPController -r &&\
  cp lib /opt/tplink/EAPController -r &&\
  cp install.sh /opt/tplink/EAPController -r &&\
  cp uninstall.sh /opt/tplink/EAPController -r &&\
  cp jre /opt/tplink/EAPController/jre -r &&\
  chmod 755 /opt/tplink/EAPController/bin/* &&\
  chmod 755 /opt/tplink/EAPController/jre/bin/* &&\
  cd /tmp &&\
  rm -rf /tmp/Omada_Controller_v3.1.4_linux_x64最初 Omada_Controller_v3.1.4_linux_x64.tar.gz.zip Omada_Controller_v3.1.4_linux_x64.tar.gz &&\
  groupadd -g 508 omada &&\
  useradd -u 508 -g 508 -d /opt/tplink/EAPController omada &&\
  mkdir /opt/tplink/EAPController/logs /opt/tplink/EAPController/work &&\
  chown -R omada:omada /opt/tplink/EAPController/data /opt/tplink/EAPController/logs /opt/tplink/EAPController/work

USER omada
WORKDIR /opt/tplink/EAPController
EXPOSE 8043/tcp 8088/tcp 27001/udp 27002/tcp 29810/udp 29811/tcp 29812/tcp 29813/tcp
VOLUME ["/opt/tplink/EAPController/data","/opt/tplink/EAPController/work","/opt/tplink/EAPController/logs"]
CMD ["/opt/tplink/EAPController/jre/bin/java","-server","-Xms128m","-Xmx1024m","-XX:MaxHeapFreeRatio=60","-XX:MinHeapFreeRatio=30","-XX:+HeapDumpOnOutOfMemoryError","-XX:-UsePerfData","-Deap.home=/opt/tplink/EAPController","-cp","/opt/tplink/EAPController/lib/*:","com.tp_link.eap.start.EapLinuxMain"]
