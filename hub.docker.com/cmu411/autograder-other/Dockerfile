FROM cmu411/autograder:latest

#----------
# SWIFT INSTALLATION
#----------
ENV swift_version=swift-5.0.1
ENV swift_filename=$swift_version-RELEASE-ubuntu18.04
RUN curl https://swift.org/builds/$swift_version-release/ubuntu1804/$swift_version-RELEASE/$swift_filename.tar.gz -LO && \
  tar -xzf $swift_filename.tar.gz && \
  sudo mv $swift_filename /opt/swift && \
  rm $swift_filename.tar.gz && \
  ln -s /opt/swift/usr/bin/swiftc /usr/local/bin/

#--------------
# MISC PACKAGE INSTALLATION -- common to all Dockerfiles
# Add convenience packages for students using container.
# The Swift starter code uses bison and flex.
#--------------
RUN apt-get update && apt-get install -y \
  bison \
  emacs \
  flex \
  gdb \
  python3 \
  vim \
  ;
