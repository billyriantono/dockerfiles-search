FROM ubuntu:bionic as builder
WORKDIR /compile
RUN sed -i -- 's/#deb-src/deb-src/g' /etc/apt/sources.list && sed -i -- 's/# deb-src/deb-src/g' /etc/apt/sources.list && \
apt-get update && apt-get build-dep nut -y && apt-get install git checkinstall -y && \
git clone https://github.com/networkupstools/nut.git && cd nut && \
./autogen.sh && \
./configure --includedir=/usr/include --mandir=/usr/share/man \
--infodir=/usr/share/info --sysconfdir=/etc/nut --localstatedir=/var \
--libexecdir=/usr/lib/nut --srcdir=. --enable-maintainer-mode \
--disable-silent-rules --libdir=/usr/lib/`gcc -print-multiarch` \
--with-ssl --with-nss --with-cgi --with-dev --enable-static \
--with-statepath=/var/run/nut --with-altpidpath=/var/run/nut \
--with-drvpath=/lib/nut --with-cgipath=/usr/lib/cgi-bin/nut \
--with-htmlpath=/usr/share/nut/www --with-pidpath=/var/run/nut \
--datadir=/usr/share/nut --with-pkgconfig-dir=/usr/lib/`gcc -print-multiarch`/pkgconfig --with-udev-dir=/lib/udev \
--with-systemdsystemunitdir=/lib/systemd/system && \
make -j 2 && checkinstall -y --pkgname=nut --type=debian --install=no --deldoc=yes --deldesc=yes --delspec=yes

FROM ubuntu:bionic
RUN apt-get update && apt-get install lsb-base init-system-helpers libc6 libnspr4 libnss3 libusb-0.1-4 libwrap0 udev -y && \
mkdir /install && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
VOLUME ["/etc/nut"]
EXPOSE 3493
COPY --from=builder /compile/nut/*.deb /install
COPY init.sh .
COPY conf/ /etc/nut/
RUN dpkg -i /install/*.deb && rm -rf /install && chmod +x init.sh && mkdir -m 700 /var/run/nut && chmod 700 /etc/nut/* -R
ENV PATH="/usr/local/ups/sbin/:/usr/local/ups/bin/:${PATH}"
ENTRYPOINT ["./init.sh"]
