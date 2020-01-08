FROM replikation/debian_basic
MAINTAINER Christian Brandt <christian.jena@gmail.com>

RUN DWNL=$(curl -s https://github.com/ablab/spades/releases | grep "Linux.tar.gz" | head -1 | cut -f2 -d'"') && wget https://github.com/${DWNL}
RUN /bin/bash -c "tar -xf *tar.gz"
RUN /bin/bash -c "rm -f *tar.gz"
RUN /bin/bash -c "mv /SPAdes-*/ /SPAdes/"
WORKDIR /usr/bin
RUN ln -T python3 python
ENV PATH /SPAdes/bin:$PATH
