FROM centos
WORKDIR /tmp
RUN yum install -y bzip2 wget git curl curl-devel vim gcc python python-devel zsh \
    tar bzip2 gcc-c++ readline-devel gmp-devel gcc-gfortran cmake zlib zlib-devel \
    mysql mysql-devel libpng libpng12 libpng-devel libtiff libtiff-devel libjpeg \
    libjpeg-devel openssh-server openssh-clients boost boost-devel inetutils-ping iproute net-tools \
    initscripts cairo cairo-devel cairomm-devel libjpeg-turbo libjpeg-turbo-devel pango pango-devel \
    pangomm pangomm-devel libXt libXt-devel iptables-services openssl-devel openssl && yum clean all && rm -rf /tmp/* /var/tmp/*
RUN wget https://download2.rstudio.org/server/centos6/x86_64/rstudio-server-rhel-1.2.1335-x86_64.rpm \
    && yum install -y rstudio-server-rhel-1.2.1335-x86_64.rpm && yum clean all && rm -rf /tmp/* /var/tmp/*
RUN wget https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/Anaconda3-5.3.1-Linux-x86_64.sh
RUN cd /tmp \
    && bash Anaconda3-5.3.1-Linux-x86_64.sh -b -p /opt/anaconda \
    && /opt/anaconda/bin/conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/bioconda/ \
    && /opt/anaconda/bin/conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/ \
    && /opt/anaconda/bin/conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/ \
    && /opt/anaconda/bin/conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r/ \
    && /opt/anaconda/bin/conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/mro/ \
    && /opt/anaconda/bin/conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/ \
    && /opt/anaconda/bin/conda config --set show_channel_urls yes
ENV PATH=/opt/anaconda/bin/:$PATH
RUN conda install -y conda-build
RUN conda clean -y -all
RUN yum install -y epel-release
RUN yum install -y R && yum clean all && rm -rf /tmp/* /var/tmp/*
RUN R -e "install.packages(\"rmarkdown\",repos=\"https://mirrors.tuna.tsinghua.edu.cn/CRAN/\")"
RUN mkdir /var/run/sshd
RUN echo 'root:root' | chpasswd
RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd
ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile
RUN ssh-keygen -t dsa -f /etc/ssh/ssh_host_dsa_key && ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key
RUN echo 'auth-minimum-user-id=0' >> /etc/rstudio/rserver.conf && \
    echo 'www-port=8787' >>/etc/rstudio/rserver.conf && \
    echo 'www-port=8787' >>/etc/rstudio/rsession.conf
RUN systemctl enable iptables && echo "-A INPUT -p tcp -m state --state NEW -m tcp --dport 8787 -j ACCEPT" >>/etc/sysconfig/iptables
RUN sed -i 's#500#0#g' /etc/pam.d/rstudio
RUN ln -sf /opt/anaconda/lib/libstdc++.so.6  /lib64/libstdc++.so.6 && \
    ln -fs /opt/anaconda/lib/libz.so.1 /lib64/libz.so.1
EXPOSE 8787 22 8888 8080 9090
ADD container.profile /root/.bash_profile
RUN localedef -c -f UTF-8 -i zh_CN zh_CN.UTF-8
ENV LANG zh_CN.UTF-8
ENV LC_ALL zh_CN.UTF-8
ENV USER=root
RUN R -e "install.packages(c(\"dplyr\",\"rprojroot\"),repos=\"https://mirrors.tuna.tsinghua.edu.cn/CRAN/\")"
RUN R -e "install.packages(c(\"reshape2\",\"ggplot2\"),repos=\"https://mirrors.tuna.tsinghua.edu.cn/CRAN/\")"
COPY entrypoint.sh entrypoint.sh
CMD ./entrypoint.sh
