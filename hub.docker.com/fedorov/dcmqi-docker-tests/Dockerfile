FROM fedora:latest

RUN yum -y groups install "Development Tools"
RUN yum -y install cmake
RUN yum -y install gcc-c++

RUN mkdir /home/work
RUN cd /home/work && git clone https://github.com/fedorov/dcmqi.git && cd dcmqi && git checkout add-cxx-standard-property && cd .. && mkdir dcmqi-build
RUN cd /home/work/dcmqi-build && cmake ../dcmqi && make -j4 DCMTK && make -j4 ITK

ENTRYPOINT ["/bin/bash"]


