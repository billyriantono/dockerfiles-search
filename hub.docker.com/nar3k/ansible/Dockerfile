FROM williamyeh/ansible:alpine3-onbuild
RUN apk update
RUN apk add git gcc g++ libxml2 libxml2-dev py-lxml py-pip python-dev
RUN pip install lxml junos-eznc pyvmomi nsxramlclient pysnmp docker-py napalm pan-python pandevice pymongo jxmlease dnspython
RUN ansible-galaxy install Juniper.junos PaloAltoNetworks.paloaltonetworks
CMD mkdir /ansible
CMD mkdir /modules
WORKDIR /modules
RUN git clone https://github.com/vmware/nsxansible.git
RUN git clone https://github.com/napalm-automation/napalm-ansible.git
COPY ansible.cfg /etc/ansible
WORKDIR /ansible
