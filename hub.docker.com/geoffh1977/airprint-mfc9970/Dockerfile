# Add Printer Drivers To Airprint Container
FROM geoffh1977/airprint:latest
LABEL maintainer="geoffh1977 <geoffh1977@gmail.com>"

# Install Brother Drivers From Repository
RUN apt-get update && \
    apt-get install --no-install-recommends -y brother-lpr-drivers-extra brother-cups-wrapper-extra && \
	rm -rf /var/lib/apt/lists/*

# Add Specific Drivers
COPY binaries/mfc9970cdwcupswrapper-1.1.1-5.i386.deb /tmp/
COPY binaries/mfc9970cdwlpr-1.1.1-5.i386.deb /tmp/
RUN dpkg -i --force-all /tmp/mfc9970cdwlpr-1.1.1-5.i386.deb && \
    dpkg -i --force-all /tmp/mfc9970cdwcupswrapper-1.1.1-5.i386.deb
