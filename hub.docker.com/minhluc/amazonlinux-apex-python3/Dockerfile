FROM amazonlinux:latest
RUN yum install -y golang make git gcc gcc-c++ freetype-devel yum-utils openssl-devel groupinstall development wget which python-devel findutils zlib-devel zip tar gzip
RUN amazon-linux-extras install -y python3=3.6.2
RUN curl https://bootstrap.pypa.io/get-pip.py | python - 'pip==18.0.0'
RUN curl https://raw.githubusercontent.com/apex/apex/master/install.sh | sh
RUN pip3 install virtualenv
RUN echo "export GOROOT=/usr/lib/golang" >> ~/.bash_profile
RUN echo "export GOPATH=$HOME/projects" >> ~/.bash_profile
RUN echo "export PATH=$PATH:$GOROOT/bin" >> ~/.bash_profile
RUN source ~/.bash_profile
RUN go version
RUN git clone https://github.com/direnv/direnv
RUN cd ./direnv && make && make install
RUN eval "$(direnv hook bash)" >> ~/.bashrc
RUN rm -rf ./direnv


#RUN ls -l ./direnv
#RUN cd /tmp/
#RUN wget https://dl.google.com/go/go1.11.linux-amd64.tar.gz && tar -xvf go1.11.linux-amd64.tar.gz
#RUN ls -l
#RUN cd ./go/bin && ls -l
#RUN ./go/bin/go version
#RUN chmod +x ./go/bin/*  && mv ./go/bin/* /usr/local &&  go version
#RUN cd direnv && make && make install

# RUN pip3 install aws
