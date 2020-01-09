FROM jfkhatesdocker/omnetpp_env:latest

WORKDIR "/home"

RUN git clone --branch v4.1.0 --depth 1 https://github.com/inet-framework/inet.git

RUN cd inet && make makefiles && make -j8
