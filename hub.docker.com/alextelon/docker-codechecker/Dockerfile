FROM ubuntu:16.04

#This is used to make sure we dont get any questions about installing recommended extras, if I recall correctly
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends apt-utils \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

#some musts and some nice to haves
RUN apt-get update \
        && apt-get -y install \
        sudo \
        git \
        wget \
        curl \
        && apt-get clean \
        && rm -rf /var/lib/apt/lists/*

RUN git config --global user.email "alex.telon@gmail.com" \
    && git config --global user.name "Alex Telon" 

USER root
#No, I dont use the password "work" anywhere else
RUN useradd -ms /bin/bash alex \
    && echo alex:work | chpasswd \
    && adduser alex sudo

###The above should not change often at all

#stuff for codechecker editing
RUN apt-get update && apt-get -y install clang-3.8 clang-tidy-3.8 doxygen build-essential thrift-compiler gcc-multilib python-pip autoconf libtool-bin emacs24 \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

###The above should now change too often.
# below are the more lightweight stuff that can change more often

WORKDIR /home/alex/

#clang-tidy creates a clang-tidy link, but clang does not so we have to do this manually
RUN ln -s /usr/bin/clang-3.8 /usr/bin/clang
RUN echo "export PATH=$PATH:/home/alex/codechecker_package/CodeChecker/bin/" >> /home/alex/.bashrc

#These parts below will not be cached and hence be executed everytime you build an image
RUN mkdir fork \
    && cd fork \
    && git clone https://github.com/AlexTelon/codechecker.git \
    && cd /home/alex/

RUN git clone https://github.com/Ericsson/codechecker.git \
    && cd codechecker \
    && pip install -r .ci/basic_python_requirements \
    && ./build_package.py -o /home/alex/codechecker_package

USER alex
CMD /bin/bash
ENTRYPOINT
