FROM ubuntu:16.04
MAINTAINER angel.cancio@gmail.com

# Suppress debconf warnings
ENV DEBIAN_FRONTEND noninteractive

# Switch account to root and adding user accounts and password
USER root
RUN echo "root:toor" | chpasswd

# Define home, psrhome, OSTYPE and create the directory
ENV HOME /home/qubic
ENV QUBICHOME $HOME/data
ENV OSTYPE linux

# Create qubic user which will be used to run commands with reduced privileges.
RUN adduser --disabled-password --gecos 'unprivileged user' qubic && \
    echo "qubic:qubic" | chpasswd && \
    mkdir -p $HOME/.ssh && \
    chown -R qubic:qubic /home/qubic/.ssh


# Create space for ssh deamon and update the system
RUN echo 'deb http://us.archive.ubuntu.com/ubuntu xenial main universe multiverse' >> /etc/apt/sources.list && \
    mkdir /var/run/sshd && \
    apt-get check && \
    apt-get update && \
    apt-get install -y apt-utils apt-transport-https software-properties-common python-software-properties && \
    apt-get -y upgrade

RUN apt-get -y install \
    autoconf \
    automake \
    autotools-dev \
    binutils-dev \
    bison \
    build-essential \
    cmake \
    cmake-curses-gui \
    cmake-data \
    cpp \
    csh \
    curl \
    cvs \
    cython \
    dkms \
    exuberant-ctags \
    f2c \
    fftw-dev \
    fftw2 \
    flex \
    fort77 \
    g++ \
    gawk \
    gcc \
    gfortran \
    ghostscript \
    ghostscript-x \
    git \
    git-core \
    gnuplot \
    gnuplot-x11 \
    gsl-bin \
    gv \
    h5utils \
    hdf5-helpers \
    hdf5-tools \
    hdfview \
    htop \
    hwloc \
    libatlas-dev \
    libbison-dev \
    libblas-common \
    libblas-dev \
    libblas3 \
    libboost-program-options1.58-dev \
    libboost-python1.58-dev \
    libboost-regex1.58-dev \
    libboost-system1.58-dev \
    libboost1.58-all-dev \
    libboost1.58-dev \
    libboost1.58-tools-dev \
    libc-dev-bin \
    libc6-dev \
    libcfitsio-bin \
    libcfitsio-dev \
    libcfitsio-doc \
    libcfitsio2 \
    libcfitsio3-dev \
    libcloog-isl4 \
    libcppunit-dev \
    libcppunit-subunit-dev \
    libcppunit-subunit0 \
    libfftw3-3 \
    libfftw3-bin \
    libfftw3-dbg \
    libfftw3-dev \
    libfftw3-double3 \
    libfftw3-long3 \
    libfftw3-quad3 \
    libfftw3-single3 \
    libfreetype6 \
    libfreetype6-dev \
    libgd-dev \
    libgd2-xpm-dev \
    libgd3 \
    libglib2.0-0 \
    libglib2.0-dev \
    libgmp3-dev \
    libgsl-dev \
    libgsl2 \
    libgtksourceview-3.0-dev \
    libgtksourceview2.0-dev \
    libhdf5-10 \
    libhdf5-cpp-11 \
    libhdf5-dev \
    libhdf5-serial-dev \
    libhwloc-dev \
    liblapack-dev \
    liblapack-pic \
    liblapack-test \
    liblapack3 \
    liblapacke \
    liblapacke-dev \
    libltdl-dev \
    libltdl7 \
    liblua5.1-0 \
    liblua5.1-0-dev \
    liblua5.2-0 \
    liblua5.2-dev \
    liblua5.3-0 \
    liblua5.3-dev \
    libncurses5-dev \
    libntrack-qt4-1 \
    libopenblas-base \
    libopenblas-dev \
    libpng++-dev \
    libpng-sixlegs-java \
    libpng-sixlegs-java-doc \
    libpng12-0 \
    libpng12-dev \
    libpng3 \
    libpnglite-dev \
    libpth-dev \
    libqt4-dbus \
    libqt4-declarative \
    libqt4-designer \
    libqt4-dev \
    libqt4-dev-bin \
    libqt4-help \
    libqt4-network \
    libqt4-opengl \
    libqt4-opengl-dev \
    libqt4-qt3support \
    libqt4-script \
    libqt4-scripttools \
    libqt4-sql \
    libqt4-sql-mysql \
    libqt4-svg \
    libqt4-test \
    libqt4-xml \
    libqt4-xmlpatterns \
    libqt4pas-dev \
    libqt4pas5 \
    libreadline6 \
    libreadline6-dev \
    libsocket++-dev \
    libsocket++1 \
    libsource-highlight-qt4-3 \
    libssl-dev \
    libtool \
    libx11-dev \
    llvm-4.0 \
    llvm-4.0-dev \
    llvm-4.0-doc \
    llvm-4.0-examples \
    llvm-4.0-runtime \
    locate \
    lsof \
    m4 \
    make \
    man \
    mc \
    nano \
    nfs-common \
    numactl \
    openssh-server \
    pbzip2 \
    pgplot5 \
    pkg-config \
    pkgconf \
    python \
    python-dev \
    python-setuptools \
    python-dev \
    pyqt4-dev-tools \
    python-qt4 \
    python-qt4-dbus \
    python-qt4-dev \
    python-tk \
    qt4-default \
    qt4-linguist-tools \
    qt4-qmake \
    qt4-qtconfig \
    screen \
    source-highlight \
    source-highlight-ide \
    subversion \
    swig2.0 \
    tcsh \
    tk \
    tk-dev \
    tmux \
    vim \
    wcslib-dev \
    wcslib-tools \
    wget \
    zlib1g-dev

RUN curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
RUN python get-pip.py

RUN pip install pip -U && \
    pip install setuptools -U && \
    pip install datetime -U && \
    pip install bitstring -U && \
    pip install jupyter -U && \
    pip install jupyter_nbextensions_configurator -U && \
    pip install runipy -U && \
    pip install six -U && \
    pip install numpy -U && \
    pip install scipy -U && \
    pip install pandas -U && \
    pip install h5py -U && \
    pip install fitsio -U && \
    pip install astropy -U && \
    pip install astroplan -U && \
    pip install astropy_helpers -U && \
    pip install astroquery -U && \
    pip install pytz -U && \
    pip install paramz -U && \
    pip install APLpy -U && \
    pip install pyfits -U && \
    pip install cycler -U && \
    pip install peakutils -U && \
    pip install matplotlib -U && \
    pip install seaborn -U && \
    pip install lmfit -U && \
    pip install pyephem -U && \
    pip install numexpr -U

RUN pip install --ignore-installed --no-deps pysimulators==1.1.4
RUN pip install --ignore-installed --no-deps pyoperators==0.13.16
#RUN pip install git+https://github.com/qubicsoft/qubic.git
RUN pip install -U https://github.com/qubicsoft/qubic/archive/master.zip

# Switch account to qubic
USER qubic

RUN mkdir -p $HOME/.jupyter
RUN echo "c.NotebookApp.token = u''" >> $HOME/.jupyter/jupyter_notebook_config.py

RUN mkdir -p $QUBICHOME && \
    chown -R qubic:qubic $QUBICHOME

#RUN jupyter contrib nbextension install --user
ENTRYPOINT cd $QUBICHOME && jupyter-notebook --ip='*' --no-browser

