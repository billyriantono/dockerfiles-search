FROM ubuntu:16.04

# Install the things we need
RUN apt-get update && apt-get install -y \
  build-essential \
  git \
  openssl \
  vim

# Clone the demo repo
RUN git clone https://bitbucket.org/lastzulu/crypt_demo.git 
  
# Build all the things
RUN cd crypt_demo \
  && make openssl \
  && make all  

# Run with:
# docker run -it <image> bash
