FROM cmhi/cuda9.0-cudnn7


RUN pip install --upgrade pip


# Add symbol link for libcuda.so
RUN ln -s /usr/local/cuda/targets/x86_64-linux/lib/stubs/libcuda.so \
          /usr/local/cuda/targets/x86_64-linux/lib/stubs/libcuda.so.1

#update and upgrade, install git
RUN apt-get update && apt-get upgrade -y && apt-get -y install git && apt-get install -y vim

ENV LC_ALL C

#if you want to build the docker image with data, please prepare the data first and remove the '#' in next line
#ADD ./data /tmp/data

WORKDIR /root