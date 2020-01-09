FROM ubuntu:16.10

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

USER root
#No, I dont use the password "work" anywhere else
RUN useradd -ms /bin/bash alex \
    && echo alex:work | chpasswd \
    && adduser alex sudo

RUN git config --global user.email "alex.telon@gmail.com" \
    && git config --global user.name "Alex Telon" 

###The above should not change often at all

#more nice-to-haves
RUN apt-get update \
        && apt-get -y install \
        emacs24 \
        && apt-get clean \
        && rm -rf /var/lib/apt/lists/*

USER alex

RUN touch derp

CMD /bin/bash
ENTRYPOINT
