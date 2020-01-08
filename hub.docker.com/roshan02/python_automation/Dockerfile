FROM ubuntu:latest
ENV TERM linux
WORKDIR /root
RUN apt update
RUN apt-get install -y wget
RUN apt-get install -y git
## https://github.com/vmware/vsphere-automation-sdk-python 
##Installing pyvmomi as it is required as a dependecy for running some sample files mentioned in the sdk github page

RUN apt-get install -y python-pip
RUN pip install --upgrade pip setuptools
RUN pip install --upgrade git+https://github.com/vmware/vsphere-automation-sdk-python.git

RUN pip install pyvmomi
## not sure why am I clonning this, copied this step from the pyvmomi Docker file.
RUN git clone https://github.com/vmware/pyvmomi.git 
RUN git clone https://github.com/vmware/vsphere-automation-sdk-python

##INSTALLER FILES DEFINITION -- defining the file names in the local and env varibles
ENV VSPHERE65_AUTOMATION_SDK_PYTHON=VMware-vSphere-Automation-SDK-Python-6.5.0-4571810.zip
ENV VMWARE_UTILS_INSTALLER=installerFile_pythonautomationsdk.sh
ENV VSPHERE65_MGMT_SDK=VMware-vSphere-SDK-6.5.0-4571253.zip									

## giving the permissions to edit the file. 
COPY installerFile_pythonautomationsdk.sh /tmp/
RUN chmod +rwx /tmp/$VMWARE_UTILS_INSTALLER 

#COPY installerFile_pythonautomationsdk.sh /tmp/ 

# downloading the python automation sdk. copied from 

RUN /tmp/$VMWARE_UTILS_INSTALLER


CMD ["/bin/bash"]

