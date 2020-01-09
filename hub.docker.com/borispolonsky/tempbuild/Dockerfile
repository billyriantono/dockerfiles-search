FROM tensorflow/tensorflow:2.0.0-gpu-py3
RUN apt-get update && apt-get install -y openssl libssl-dev zlib1g-dev libbz2-dev && rm -rf /var/lib/apt/lists/*
RUN pip3 install -U pyyaml pip zeroc-ice
CMD /bin/bash
