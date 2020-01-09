FROM cmu411/autograder:latest

#--------------
# HASKELL INSTALLATION
#--------------
# The -L flag to curl follows redirects.
ENV haskell_version=lts-13.29
RUN apt-get update && apt-get install -y \
    libgmp-dev \
    xz-utils \
  && \
  curl -L https://get.haskellstack.org/stable/linux-x86_64.tar.gz -O && \
  tar xf linux-x86_64.tar.gz && \
  cp stack-*-linux-x86_64/stack /usr/bin/stack && \
  rm linux-x86_64.tar.gz && \
  rm -r stack-*-linux-x86_64 && \
  stack setup --resolver "$haskell_version"

#--------------
# HASKELL PACKAGE INSTALLATION
#--------------
RUN stack install --resolver $haskell_version \
  alex \
  array \
  base \
  bifunctors \
  bytestring \
  Cardinality \
  containers \
  deepseq \
  fgl \
  filepath \
  happy \
  heap \
  lens \
  llvm-hs-7.0.1 \
  mtl \
  primitive \
  process \
  pqueue \
  psqueues \
  split \
  syb \
  test-framework \
  test-framework-hunit \
  test-framework-quickcheck2 \
  transformers \
  unordered-containers \
  utf8-string \
  vector \
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
