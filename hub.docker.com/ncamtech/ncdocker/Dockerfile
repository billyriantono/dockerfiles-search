FROM nvidia/cuda:8.0-devel-ubuntu14.04

# Update apt and get the various package we need
RUN apt-get -y update                          \
                                            && \
    apt-get install -y --no-install-recommends \
       build-essential                         \
       cmake3                                  \
       clang-3.9                               \
       curl                                    \
       git                                     \
       freeglut3                               \
       freeglut3-dev                           \
       libatlas-base-dev                       \
       libcairo2                               \
       libgdk-pixbuf2.0-0                      \
       libgtk-3-0                              \
       libjasper1                              \
       libmng-dev                              \
       libssl-dev                              \
       libsuitesparse-dev                      \
       libtbb-dev                              \
       libudev-dev                             \
       python                                  \
       python-setuptools                       \
       python-dev                              \
                                            && \
    apt-get install -y --no-install-recommends \
       libqt4-dev                              \
       libqt4-core                             \
       libqt4-gui                              \
       libqt4-xml                              \
       libqt4-opengl                           \
       libqt4-dev-bin                          \
       libqt4-opengl-dev                       \
       qt4-qmake                               \
       qt4-dev-tools                           \
                                            && \
    rm -rf /var/lib/apt/lists/*

# Download and unpack the libs-meta pre-packed binaries
RUN curl -k -L https://www.dropbox.com/s/krdj533gyvw70js/libraries-meta-linux-2018_07_20__09_57_24.tgz \
    | tar -xz

RUN printf "export NC_LIBRARIES_META=/libraries-meta\n" >> ~/.bashrc
RUN printf "export TEST_REPORTS_DIR=~/test-reports\n" >> ~/.bashrc

# Ensure we have pip
RUN python -m easy_install pip
# Ensure we have virtualenv
RUN python -m pip install --upgrade virtualenv
