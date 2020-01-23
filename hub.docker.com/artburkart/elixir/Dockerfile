FROM buildpack-deps:wheezy
MAINTAINER Arthur Burkart <arturkart@gmail.com>

# Set up environment variables
ENV DEBIAN_FRONTEND noninteractive
ENV LANG C.UTF-8
ENV OTP_VERSION 18.1
ENV ELIXIR_VERSION 1.0.5
ENV PATH $PATH:/elixir/bin

# Install git
RUN apt-get update && apt-get install -y git

# Install Erlang from source
ADD http://erlang.org/download/otp_src_${OTP_VERSION}.tar.gz /usr/src/
RUN cd /usr/src \
    && tar xf otp_src_${OTP_VERSION}.tar.gz \
    && cd otp_src_${OTP_VERSION} \
    && ./configure \
    && make -j8 \
    && make install \
    && rm -rf /usr/src/otp_src_${OTP_VERSION} && rm /usr/src/otp_src_${OTP_VERSION}.tar.gz \
    && rm -rf /var/lib/apt/lists/*

# Install elixir from source
RUN git clone --depth 1 --branch v$ELIXIR_VERSION https://github.com/elixir-lang/elixir.git \
  && cd elixir \
  && make -j8 clean test

CMD ["elixir"]
