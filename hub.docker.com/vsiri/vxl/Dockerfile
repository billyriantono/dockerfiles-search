FROM debian:9

SHELL ["bash", "-euxvc"]

RUN apt-get update; \
    DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        python python-dev gcc g++ curl bzip2 rsync unzip ca-certificates \
        libglew1.10 libglu1-mesa libxmu6 libxi6 freeglut3 libgtk2.0-0 \
        libglew-dev libglu1-mesa-dev libxmu-dev libxi-dev freeglut3-dev libgtk2.0-dev \
        geotiff-bin libgeotiff-dev; \
    rm -rf /var/lib/apt/lists/*

ARG CMAKE_VERSION=3.11.0
RUN cd /tmp; \
    curl -fLO https://cmake.org/files/v${CMAKE_VERSION%.*}/cmake-${CMAKE_VERSION}-Linux-x86_64.tar.gz; \
    curl -fLo cmake.txt https://cmake.org/files/v${CMAKE_VERSION%.*}/cmake-${CMAKE_VERSION}-SHA-256.txt; \
    grep 'Linux-x86_64\.tar\.gz' cmake.txt | sha256sum -c - > /dev/null; \
    tar --strip-components=1 -xf cmake-${CMAKE_VERSION}-Linux-x86_64.tar.gz -C /usr/local; \
    rm cmake-${CMAKE_VERSION}-Linux-x86_64.tar.gz cmake.txt;

RUN cd /tmp; \
    curl -fLO http://www2.ati.com/drivers/linux-amd-14.41rc1-opencl2-sep19.zip --referer support.amd.com; \
    unzip -q linux-amd-14.41rc1-opencl2-sep19.zip; \
    rm linux-amd-14.41rc1-opencl2-sep19.zip; \
    sh fglrx-14.41/amd-driver-installer-14.41-x86.x86_64.run --extract /tmp/ati; \
    cp -dr --no-preserve=ownership /tmp/ati/arch/x86_64/* /tmp/ati/common/* /; \
    ln -s /usr/lib64/libOpenCL.so.1 /usr/lib64/libOpenCL.so; \
    echo /usr/lib64 > /etc/ld.so.conf.d/lib64.conf; \
    rm -r /tmp/fglrx-14.41 /tmp/ati; \
    ldconfig

RUN mkdir -p /usr/include/CL; \
    for x in opencl cl_platform cl cl_ext cl_gl cl_gl_ext cl_version; do \
      curl -fLo "/usr/include/CL/${x}.h" "https://raw.githubusercontent.com/KhronosGroup/OpenCL-Headers/master/CL/${x}.h"; \
    done

RUN cd /usr/bin && \
    curl -fLO https://github.com/ninja-build/ninja/releases/download/v1.7.1/ninja-linux.zip && \
    unzip ninja-linux.zip && rm ninja-linux.zip

# Install git for circle ci
RUN apt-get update; \
    DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends git ssh; \
    rm -rf /var/lib/apt/lists/*

# #Similar to https://github.com/NVIDIA/nvidia-docker/pull/146, so we somehow hardcode libGL.so?
# RUN mkdir /vxl_hack && \
#     ln -s /usr/local/nvidia/lib64/libGL.so.1 /vxl_hack/libGL.so

LABEL com.nvidia.volumes.needed="nvidia_driver"
ENV NVIDIA_VISIBLE_DEVICES=all \
    NVIDIA_DRIVER_CAPABILITIES=compute,utility

#And install the nvidia icd so that nvidia works in opencl
RUN echo libnvidia-opencl.so.1 > /etc/OpenCL/vendors/nvidia.icd && \
    echo '/usr/local/nvidia/lib64\n/vxl_hack\n/usr/local/nvidia/lib' > /etc/ld.so.conf.d/nvidia.conf

ENV PATH /usr/local/nvidia/bin:${PATH}
ENV LD_LIBRARY_PATH /usr/local/nvidia/lib:/usr/local/nvidia/lib64:/vxl_hack:${LD_LIBRARY_PATH}

ADD vxl_entrypoint.bsh /

ENTRYPOINT ["/vxl_entrypoint.bsh"]

CMD ["vxl"]