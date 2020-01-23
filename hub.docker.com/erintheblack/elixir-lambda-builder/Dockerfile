FROM amazonlinux:2017.03.1.20170812

ENV LANG="en_US.UTF-8" \
    ERL_TOP="/usr/local/otp_src_22.2" \
    PATH=$PATH:/usr/local/elixir/bin

WORKDIR /usr/local

RUN yum -y install git
RUN yum -y groupinstall "Development Tools"
RUN yum -y install ncurses-devel
RUN yum -y install openssl openssl-devel gcc-c++ unixODBC unixODBC-devel fop java-1.6.0-openjdk-devel
RUN yum -y install wget
RUN wget http://erlang.org/download/otp_src_22.2.tar.gz && \
 tar zxvf otp_src_22.2.tar.gz && rm -f otp_src_22.2.tar.gz
WORKDIR /usr/local/otp_src_22.2
RUN ./configure && make && make install

WORKDIR /usr/local

RUN git clone https://github.com/elixir-lang/elixir.git
WORKDIR /usr/local/elixir
RUN make clean install

RUN mix local.hex --force
RUN mix local.rebar --force

WORKDIR /tmp
