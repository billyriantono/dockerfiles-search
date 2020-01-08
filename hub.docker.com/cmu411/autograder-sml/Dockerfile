FROM cmu411/autograder:latest

#-----------------------
# MLton Installation
#-----------------------
ENV mlton_version=20180207
ENV mlton_pkg=mlton-$mlton_version-1.amd64-linux
RUN apt-get update && apt-get install -y \
    libgmp-dev \
  && \
  cd /opt && \
  mkdir mlton && \
  cd mlton && \
  curl https://sourceforge.net/projects/mlton/files/mlton/$mlton_version/$mlton_pkg.tgz -LO && \
  tar xvf $mlton_pkg.tgz && \
  rm $mlton_pkg.tgz && \
  make -C $mlton_pkg

#-----------------------
# C++ Library Installation
#-----------------------
RUN apt-get update && apt-get install -y \ 
    bison \ 
    flex \
    ;

#--------------
# MISC PACKAGE INSTALLATION -- common to all Dockerfiles
# Add convenience packages for students using container.
#--------------
RUN apt-get update && apt-get install -y \
  emacs \
  gdb \
  python3 \
  vim \
  ;
