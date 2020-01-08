FROM openjdk:6-jre

COPY ./SMPPSim.tar.gz /home
RUN cd /home && \
    tar -xvzf SMPPSim.tar.gz && chmod +x ./SMPPSim/startsmppsim.sh 
COPY ./smppsim.props /home/SMPPSim/conf
COPY ./deliver_messages.csv /home/SMPPSim

EXPOSE 88
EXPOSE 2775
EXPOSE 2776
EXPOSE 3333

WORKDIR /home/SMPPSim
CMD ["/bin/bash", "-c", "\"./startsmppsim.sh\""]
