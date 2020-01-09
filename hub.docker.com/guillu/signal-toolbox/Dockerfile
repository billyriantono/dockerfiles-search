# Pull base image
FROM ubuntu:18.04

# Install dependencies
RUN apt update \
    && apt install -y \
       tcsh \
       openjdk-8-jdk \
       cmake \
       gcc \
       g++ \
       wget \
    && apt clean

# Dowload the sources
RUN cd && wget http://www.irisa.fr/Polychrony/Download/SignalToolBox/releases/4.20/PolychronyToolset-SignalToolBox-4.20-linux-x86_64.tar.gz && tar -xvf PolychronyToolset-SignalToolBox-4.20-linux-x86_64.tar.gz && cd PolychronyToolset-SignalToolBox-4.20-linux-x86_64/cmake && cmake .. && cd

# Launch signal toolbox
CMD ["tcsh", "source", "PolychronyToolset-SignalToolBox-4.20-linux-x86_64/PolychronyToolset_setup"]
