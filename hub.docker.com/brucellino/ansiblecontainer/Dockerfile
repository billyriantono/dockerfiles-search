# Copyright 2016 C.S.I.R. Meraka Institute

# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#    http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

# CentOS 7 Ansible-ready docker file
FROM centos:7
MAINTAINER Bruce Becker bbecker@csir.co.za
# Install the EPEL repo
RUN rpm -ivh http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
RUN yum update -y
# This is probably a _really_ bad idea - lots of unneeded dependencies.
RUN yum -y groupinstall 'Development Tools'
# Install prerequisites
RUN  yum -y install \
            libselinux-python \
            python-devel \
            python-setuptools \
            libffi-devel \
            openssl-devel \
            which
RUN easy_install pip
# Install Ansible
RUN pip install ansible
RUN which ansible
RUN ansible --version
RUN yum clean all