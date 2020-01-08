FROM lnlssol/docker-debian9-epicsbase3_14
RUN apt-get update
RUN apt-get install libsz2 hdf5-tools libhdf5-dev libtiff5-dev libxml2-dev re2c wget make gcc g++ libusb-1.0-0-dev x11proto-core-dev libx11-dev ivtools-dev libxext-dev -y
RUN apt-get install vim -y
RUN apt-get install libusb-dev -y
RUN apt-get install git -y
COPY synapps6.sh /tmp
RUN chmod +x /tmp/synapps6.sh
RUN /tmp/synapps6.sh


WORKDIR  /usr/local/epics/synApps/support

RUN make release
RUN export PATH=$PATH:/sbin:/usr/local/epics/base/bin/linux-x86_64:/usr/local/epics/extensions/bin/linux-x86_64 && make -j12


CMD bash
