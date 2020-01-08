FROM lnlssol/debian9-epicsbase
RUN apt-get update
RUN apt-get install libsz2 hdf5-tools libhdf5-dev libtiff5-dev libxml2-dev re2c wget make gcc g++ libusb-1.0-0-dev x11proto-core-dev libx11-dev ivtools-dev libxext-dev -y
RUN apt-get install vim -y
RUN apt-get install libusb-dev -y
RUN apt-get install git -y
COPY synapps6.sh /tmp
RUN chmod +x /tmp/synapps6.sh
RUN /tmp/synapps6.sh

COPY extensions.sh /tmp
RUN /tmp/extensions.sh
