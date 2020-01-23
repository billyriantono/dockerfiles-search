FROM optiva/rhel6.4-core
LABEL maintainer="Damho Lee by Suresoft, dhlee@suresofttech.com"

RUN mkdir -p /tmp/prerequisite
WORKDIR /tmp/prerequisite
RUN curl https://nas2.ldhldh.myds.me:10081/csbuild/rhel-source.txt > rhel-source.repo
RUN cat ./rhel-source.repo
RUN cp ./rhel-source.repo /etc/yum.repos.d/rhel-source.repo
RUN yum clean metadata
RUN yum clean all
RUN rpm --import http://mirror.centos.org/centos/RPM-GPG-KEY-CentOS-6
RUN yum install -y tar bzip wget zip unzip gcc gcc-c++ glibc-static ; yum clean all
RUN yum provides */lsb_release ; yum clean all
RUN yum install -y redhat-lsb ; yum clean all
RUN curl https://nas2.ldhldh.myds.me:10081/csbuild/prerequisite_packages_installer_CSBUILD.zip > prerequisite_packages_installer_CSBUILD.zip
RUN unzip prerequisite_packages_installer_CSBUILD.zip
RUN sh ./install.sh
RUN chmod +x ./src/cmake-3.3.2-Linux-x86_64.sh
RUN echo "y" > input
RUN ./src/cmake-3.3.2-Linux-x86_64.sh --prefix=/usr/local < input
RUN ln -s /usr/local/bin/python3.6 /usr/local/bin/python3
RUN cp -rf /usr/local/cmake-3.3.2-Linux-x86_64/bin ../
RUN cp -rf /usr/local/cmake-3.3.2-Linux-x86_64/doc ../
RUN cp -rf /usr/local/cmake-3.3.2-Linux-x86_64/man ../
RUN cp -rf /usr/local/cmake-3.3.2-Linux-x86_64/share ../
RUN rm -rf /usr/local/cmake-3.3.2-Linux-x86_64
RUN pip3 install pyinstaller
RUN pip3 install requests
RUN pip3 install colorama
RUN pip3 install wcmatch
RUN pip3 install psutil
RUN pip3 install distro
RUN pip3 install hjson
RUN pip3 install lark-parser

CMD ["bash"]
