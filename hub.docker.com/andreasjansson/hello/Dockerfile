FROM    ubuntu

RUN     apt-get update
RUN     apt-get install -y ucspi-tcp

CMD     tcpserver -RHl0 -v 0.0.0.0 $PORT sh -c "echo $MESSAGE"
