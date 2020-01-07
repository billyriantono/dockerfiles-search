FROM ubuntu:16.04

    
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
RUN echo "deb http://download.mono-project.com/repo/ubuntu vs-xenial main" | tee /etc/apt/sources.list.d/mono-official-vs.list
#RUN echo "deb http://download.mono-project.com/repo/ubuntu stable-xenial main" | tee /etc/apt/sources.list.d/mono-official-vs.list

RUN apt-get update \
    && apt-get -y install mono-devel \           
    && apt-get -y install less joe git monodevelop monodevelop-nunit monodevelop-versioncontrol

RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/*

RUN mkdir /HOME

ADD entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
    
ENTRYPOINT ["/entrypoint.sh"]
CMD [":0"]
