#Note: Ruby 1.8.6 patches obtained from https://github.com/rvm/rvm/tree/master/patches/ruby/1.8.6 and based on default patchset by rvm in https://github.com/rvm/rvm/blob/master/patchsets/ruby/1.8.6/default
FROM jolicode/rbenv

# Install older openssl
RUN cd $HOME && wget http://www.openssl.org/source/openssl-0.9.8zb.tar.gz
RUN cd $HOME && tar ixzf openssl-0.9.8zb.tar.gz && rm openssl-0.9.8zb.tar.gz
RUN cd $HOME/openssl-0.9.8zb && ./config && make

ADD patches/ $HOME/patches

RUN rbenv -v

RUN cat $HOME/patches/* | \
    CFLAGS="-O2 -fno-tree-dce -fno-optimize-sibling-calls" RUBY_CONFIGURE_OPTS="--with-openssl-dir=$HOME/openssl-0.9.8zb" MAKEOPTS="" \
    rbenv install --patch  1.8.6-p383 && \
    rbenv global 1.8.6-p383

# Add gem settings
RUN echo 'gem: --no-rdoc --no-ri' >> /$HOME/.gemrc
