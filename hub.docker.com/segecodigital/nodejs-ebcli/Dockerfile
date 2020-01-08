FROM node:8

RUN apt-get update && \
    apt-get install -y \
        python-pip \
        python-dev
 
RUN pip install awscli

CMD ["/bin/bash"]
