FROM ubuntu:bionic

ADD 'https://download.virtualbox.org/virtualbox/6.0.6/virtualbox-6.0_6.0.6-130049~Ubuntu~bionic_amd64.deb' vb.deb
ADD 'https://download.virtualbox.org/virtualbox/6.0.6/Oracle_VM_VirtualBox_Extension_Pack-6.0.6.vbox-extpack' .
RUN apt-get -qq update && apt-get install kmod ./vb.deb --yes --no-install-recommends
RUN echo y | VBoxManage extpack install Oracle_VM_VirtualBox_Extension_Pack-6.0.6.vbox-extpack > /dev/null
RUN rm vb.deb *.vbox-extpack

RUN apt-get install wget --yes --no-install-recommends

RUN useradd -ms /bin/bash vm --groups vboxusers
WORKDIR /home/vm
COPY --chown=vm:vm assets/ .

USER vm
ENTRYPOINT ["/home/vm/entrypoint.sh"]