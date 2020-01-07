FROM jsums/msf-openvas
MAINTAINER Ashley Abraham "ashley.abraham@jsums.edu"

ENV DEBIAN_FRONTEND noninteractive
     
RUN curl -sSL https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -o /tmp/miniconda.sh \
    && bash /tmp/miniconda.sh -bfp /usr/local \
    && rm -rf /tmp/miniconda.sh \ 
    && conda update conda
    
ENV PATH /usr/local/bin:$PATH

# Attach this container to stdin when running, like this:
# docker run --net=host -t -i jsums/msf-openvas-conda
#--net=host allows listening to incoming connections on the host ip

ADD ./init.sh /init.sh
RUN chmod +x /init.sh
ENTRYPOINT ./init.sh
