FROM fedora:latest
RUN yum -y install cmake gcc gnu-getopt java-1.8.0-openjdk libpng-devel fontforge-devel cairo-devel poppler-devel libspiro-devel freetype-devel  poppler-data libjpeg-turbo-devel git make gcc-c++
RUN git clone git://github.com/coolwanglu/pdf2htmlEX.git
RUN cd pdf2htmlEX && cmake . && make && make install && yum clean all
CMD ["bash"]
