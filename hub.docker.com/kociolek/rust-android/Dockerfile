FROM opinionatedgeek/android-ndk-r10e
MAINTAINER Marcin Kocot "kociolek.farfocle@gmail.com"

# We should import it somehow
ENV ANDROID_NDK_ROOT /opt/android-ndk-r10e

#Base image drops root user, bring it back
User root
## needed by cargo
ENV USER root

# Install NDK
# Update the system and install essential tools.
RUN apt-get update && apt-get install -yq curl \
                                 	  gdb \
				 	  g++ \
					  python
                                  #g++-multilib \
                                  #lib32stdc++6 \
                                  #libssl-dev \
                                  #libncurses5-dev

ENV triple x86_64-unknown-linux-gnu
# install cargo
RUN curl -sL https://static.rust-lang.org/cargo-dist/cargo-nightly-$triple.tar.gz | tar xvz -C /tmp
RUN /tmp/cargo-nightly-$triple/install.sh
# cleanup package manager
RUN apt-get remove --purge -y curl && apt-get autoclean && apt-get clean
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# prepare dir
# TODO: use git to fetch source?
RUN mkdir /source && \
    cd /source && \
    wget https://static.rust-lang.org/dist/rustc-nightly-src.tar.gz && \
    tar -xvzf rustc-nightly-src.tar.gz
RUN rm /source/rustc-nightly-src.tar.gz
# source/rustc-nightly

# Switch to bash, android seems to love it too much
CMD ["bash"]
# Create standalone ndk compiler
RUN $ANDROID_NDK_ROOT/build/tools/make-standalone-toolchain.sh \
    --platform=android-9 \
    --install-dir=/opt/ndk_standalone \
    --arch=arm \
    --system=linux-x86_64
# Now build time!
WORKDIR /source/rustc-nightly

# Lets not get too optimistic for python path, config like to pick android one
RUN export PATH=$PATH:/opt/ndk_standalone/bin && \
    cd /source/rustc-nightly && \
    ./configure --target=arm-linux-androideabi --prefix=/usr/local

# I dont see any way to get around using only single make to build whole 
# rustc. 
RUN make -j`nproc`
RUN make install

VOLUME ["/source"]
WORKDIR /source
