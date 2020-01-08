FROM ubuntu

RUN apt update

RUN apt install -y git

RUN apt install -y python3

RUN mkdir Jenkins

RUN cd Jenkins

RUN git clone https://github.com/MNA2406/Jenkins-pipe.git

RUN python3 --version

RUN cd Jenkins-pipe

RUN pwd

RUN ls Jenkins-pipe

CMD  [ 'python3' 'Jenkins-pipe/serv.py' ]

EXPOSE 8000
 

