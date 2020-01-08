FROM ubuntu:18.04
ENV DEBIAN_FRONTEND noninteractive

#Install all the requirements
RUN apt-get update -qq && apt-get install -y curl git build-essential \
    python-minimal zlib1g-dev libssl-dev libreadline-dev \
    libyaml-dev libcurl4-openssl-dev \
    libffi-dev \
    libcurl4-openssl-dev \
    libxml2-dev libxslt-dev \
    ffmpeg libpq-dev \
    libfftw3-dev libmagickwand-dev libopenexr-dev liborc-0.4-0 \
    gobject-introspection libgsf-1-dev \
    libglib2.0-dev liborc-0.4-dev automake libtool swig gtk-doc-tools

# Install Node 9.x because 10.x doesn't webpack very well
RUN curl -sL https://deb.nodesource.com/setup_9.x | bash - && \
    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update && apt-get install -y nodejs yarn && \
    rm -rf /var/lib/apt/lists/*

# Build libvips from source (last resort because takes forever)
RUN git clone https://github.com/jcupitt/libvips.git && \
    cd libvips && \
    ./autogen.sh && make && make install && cd .. && rm -rf libvips

ENV VIPSHOME /usr/local
ENV LD_LIBRARY_PATH $LD_LIBRARY_PATH:${VIPSHOME}/lib
ENV PATH $PATH:${VIPSHOME}/bin
ENV PKG_CONFIG_PATH $PKG_CONFIG_PATH:${VIPSHOME}/lib/pkgconfig

# Install rbenv so that we get Ruby 2.5.1 in a happy context and can update it later

#Setup ENV variables
ENV PATH /usr/local/src/rbenv/shims:/usr/local/src/rbenv/bin:$PATH
ENV RBENV_ROOT /usr/local/src/rbenv
ENV CONFIGURE_OPTS --disable-install-doc

RUN git clone https://github.com/rbenv/rbenv.git ${RBENV_ROOT} \
    && git clone https://github.com/rbenv/ruby-build.git ${RBENV_ROOT}/plugins/ruby-build \
    && ${RBENV_ROOT}/plugins/ruby-build/install.sh

RUN echo 'eval "$(rbenv init -)"' >> /etc/profile.d/rbenv.sh

RUN rbenv install 2.5.1 \
&&  rbenv global 2.5.1
