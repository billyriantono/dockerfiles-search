#use latest armv7hf compatible debian version from group resin.io as base image
FROM resin/armv7hf-debian:stretch

#enable building ARM container on x86 machinery on the web (comment out next line if not built as automated build on docker hub) 
RUN [ "cross-build-start" ]

#labeling
LABEL maintainer="safetynet.ais@gmail.com" \
      version="V0.9.1.0" \
      description="netX based TCP/IP network interface and Debian(jessie) with netX real-time ethernet programming examples"

#version
ENV HILSCHERNETPI_NETX_TCPIP_NETWORK_INTERFACE_VERSION 0.9.1.0

#copy files
COPY "./init.d/*" /etc/init.d/ 
COPY "./driver/*" "./firmware/*" /tmp/

#do installation
RUN apt-get update  \
    && apt-get install -y openssh-server build-essential  network-manager ifupdown\
#do users root and pi    
    && useradd --create-home --shell /bin/bash pi \
    && echo 'root:root' | chpasswd \
    && echo 'pi:raspberry' | chpasswd \
    && adduser pi sudo \
    && mkdir /var/run/sshd \
    && sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config \
    && sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd \
#install netX driver and netX ethernet supporting firmware
    && dpkg -i /tmp/netx-docker-pi-drv-1.1.3.deb \
#trying to leave the ethernet lan firmware out    && dpkg -i /tmp/netx-docker-pi-pns-eth-3.12.0.8.deb \
#compile netX network daemon
    && gcc /tmp/cifx0daemon.c -o /opt/cifx/cifx0daemon -I/usr/include/cifx -Iincludes/ -lcifx -pthread \
#clean up
	&&rm -rf /tmp/* \
    && apt-get remove build-essential \
    && apt-get -yqq autoremove \
    && apt-get -y clean \
    && rm -rf /var/lib/apt/lists/*


	
#create needed folders for programming examples
RUN mkdir /home/pi/manuals /home/pi/firmwares /home/pi/driver /home/pi/includes /home/pi/sources \
          /home/pi/includes/EtherNetIP /home/pi/includes/PROFINET /home/pi/includes/EtherCAT \
          /home/pi/devicedescriptions/ \
          /home/pi/devicedescriptions/PROFINET \
          /home/pi/devicedescriptions/EtherNetIP \
          /home/pi/devicedescriptions/EtherCAT \
          /home/pi/objs
		  
	
#set the working directory for programming examples
WORKDIR /home/pi

#copy the manuals (programming examples)
COPY ./manuals/* manuals/

#copy the firmware packages (programming examples)
COPY ./firmwares/* firmwares/

#copy the include files (programming examples)
COPY examples/includes/EtherCAT/* includes/EtherCAT/
COPY examples/includes/EtherNetIP/* includes/EtherNetIP/
COPY examples/includes/PROFINET/* includes/PROFINET/
COPY examples/includes/SystemPackets.h includes/
COPY examples/includes/App.h includes/
COPY examples/includes/PacketHandlerPNS.h includes/
COPY examples/includes/PacketHandlerEIS.h includes/
COPY examples/includes/PacketHandlerECS.h includes/

#copy the device description files such as GSDML, EDS (programming examples)
COPY electronic-data-sheets/PROFINET/* devicedescriptions/PROFINET/
COPY electronic-data-sheets/EtherNetIP/* devicedescriptions/EtherNetIP/
COPY electronic-data-sheets/EtherCAT/* devicedescriptions/EtherCAT/

#copy the makefile and the application source codes (programming examples)
COPY examples/Makefile ./
COPY examples/sources/* sources/

#compile the applications (programming examples)
#RUN make

#SSH port (programming examples)
EXPOSE 22
	
#set the entrypoint
ENTRYPOINT ["/etc/init.d/entrypoint.sh"]

#set STOPSGINAL
STOPSIGNAL SIGTERM

#stop processing ARM emulation (comment out next line if not built as automated build on docker hub)
RUN [ "cross-build-end" ]