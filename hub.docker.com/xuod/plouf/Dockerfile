FROM ubuntu:latest

RUN apt-get update
# Install basic stuff (language-pack-en powerline dconf-cli emacs zsh)
RUN apt-get install -y nano wget git cmake pkg-config
# Install compilers
RUN apt-get install -y gcc-5 gfortran gfortran-5
# Install G things
RUN apt-get install -y gtk-doc-tools gobject-introspection libgirepository1.0-dev libglib2.0-dev
# Install python
RUN apt-get install -y python-numpy python-gobject python-gi-cairo

# Install dependencies
RUN apt-get install -y libgsl-dev libgmp-dev libmpfr-dev libcfitsio-dev libfftw3-dev libnlopt-dev libatlas-base-dev liblapack-dev
# sundials
RUN cd && wget http://computation.llnl.gov/projects/sundials/download/sundials-2.7.0.tar.gz && \
	tar -xvf sundials-2.7.0.tar.gz && \
	mkdir sundials-build && cd sundials-build && cmake ../sundials-2.7.0 && make && make install