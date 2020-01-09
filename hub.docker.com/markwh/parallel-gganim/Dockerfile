FROM markwh/parallel-tidyverse:latest

RUN apt-get update && apt-get install -y wget libjpeg62-turbo-dev

#install rust 
RUN wget --no-check-certificate https://static.rust-lang.org/dist/rust-1.30.0-x86_64-unknown-linux-gnu.tar.gz \
  && tar -xf rust-1.30.0-x86_64-unknown-linux-gnu.tar.gz \
  && rust-1.30.0-x86_64-unknown-linux-gnu/install.sh \
  && rm -rf rust-1.30.0*

RUN install2.r --error \
  gifski \
  farver \
  png \
  progress \
  tweenr \
  imguR \ 
  gganimate

