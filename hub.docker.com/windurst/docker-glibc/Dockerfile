FROM centos:7
ENV LAST_OS_UPDATE 2019-03-10
ENV GLIB_C 2.24
RUN yum update -y
RUN yum groupinstall "Development tools" -y
RUN yum install glibc-devel.i686 glibc-i686 wget -y
WORKDIR '/tmp'
RUN wget http://ftp.gnu.org/gnu/glibc/glibc-${GLIB_C}.tar.gz
RUN tar -xvf glibc-${GLIB_C}.tar.gz
WORKDIR '/tmp/glibc-'${GLIB_C}
RUN mkdir glibc-build
WORKDIR '/tmp/glibc-'${GLIB_C}'/glibc-build'
RUN /tmp/glibc-${GLIB_C}/configure --prefix='/usr'
RUN make
RUN make install
RUN yum groupremove "Development tools" -y
RUN yum remove glibc-devel.i686 -y
