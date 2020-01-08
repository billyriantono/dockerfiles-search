FROM marxin/gcc-docker
MAINTAINER Martin Liška

WORKDIR /abuild/linux

RUN echo "CPUs: `nproc`" && echo "MEMORY: " `cat /proc/meminfo | grep MemTotal` && cat /proc/cpuinfo | tail -n50 && df -h

RUN  GIT_SSL_NO_VERIFY=true git clone https://github.com/marxin/linux-kernel-docker.git
RUN patch -p1 < linux-kernel-docker/numa_apic.patch

RUN make -j$(nproc)
