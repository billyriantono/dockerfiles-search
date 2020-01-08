FROM ubuntu

MAINTAINER params16jan@gmail.com

#installing gcc & git
RUN apt-get update \
	&& apt-get -y install gcc \
	git 
        
# Copy C code to /src
COPY . /src

#cloning the output repo from Github
RUN cd src/ \
    && git config --global user.name "paramesh-p" \
    && git config --global user.email "params16jan@gmail.com" \
    && git clone https://paramesh-p:p2r2mesh@github.com/paramesh-p/helloworld-output.git

#syncing the host time to the container
#COPY /etc/localtime /etc/localtime
#COPY hosts /tmp/

#Build the C code
RUN cd src/ \
    && gcc helloworld.c -o hello

#running the app & saving the output & pushing the output to github
CMD sh -c './src/hello > ./src/helloworld-output/output.txt && cd src/helloworld-output/ && git add output.txt && git  commit -m "DONE" && git push origin master'

