#Download from nvidia
from nvidia/cuda:9.1-devel
# Update Software repository

RUN apt-get update
RUN apt-get install -y git make libhdf5-dev hdf5-tools wget emacs 

RUN git clone https://github.com/GPUSPH/gpusph.git
WORKDIR "/gpusph/"

COPY ./entrypoint.sh /
RUN chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
