FROM tatsushid/tinycore:6.3-x86_64

ENV vol /cwd
ENV src packer_0.8.1_linux_amd64.zip
ENV dst /usr/local/packer

RUN tce-load -wic openssl-1.0.0
RUN sudo mkdir ${dst} && cd ${dst} && sudo wget https://dl.bintray.com/mitchellh/packer/${src} -O ${src} && sudo unzip ${src} && sudo rm ${src}

VOLUME ${vol}
WORKDIR ${vol}

ENTRYPOINT [ "/usr/local/packer/packer" ]
