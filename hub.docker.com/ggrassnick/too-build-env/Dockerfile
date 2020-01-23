FROM fedora:28

RUN dnf update -y
RUN dnf install -y gcc-c++ clang cmake make boost-static boost-devel cppzmq-devel libatomic findutils
RUN dnf clean all

CMD ["/bin/bash"]