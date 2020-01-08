FROM jupyter/base-notebook:latest

USER root
RUN echo "$NB_USER ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/notebook
RUN apt-get update && \
    apt-get install -y \
            build-essential \
            libssl-dev \
            libreadline-dev \
            libtool \
            zlib1g-dev \
            gnuplot \
            less \
            git \
            autoconf \
            automake \
            --no-install-recommends && \
    rm -rf /var/lib/apt/lists/*

# required for rbczmq build
RUN sudo ln -s /usr/bin/libtoolize /usr/bin/libtool

USER $NB_USER
RUN git clone https://github.com/sstephenson/rbenv.git ~/.rbenv && \
    mkdir -p ~/.rbenv/plugins && \
    git clone https://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build

ADD ./resources/_rbenv.bash $HOME/.rbenv.bash
RUN echo 'source ~/.rbenv.bash' >> $HOME/.bash_profile
RUN echo 'source ~/.rbenv.bash' >> $HOME/.bashrc

RUN bash -lc 'rbenv install 2.4.0'
RUN bash -lc 'rbenv global 2.4.0'

RUN bash -lc 'gem install \
                  iruby \
                  rbczmq \
                  pry \
                  pry-doc \
                  awesome_print \
                  gnuplot \
                  rubyvis \
                  nyaplot \
                  '
RUN bash -lc 'iruby register'
