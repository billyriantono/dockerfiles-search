FROM finalduty/archlinux:daily
RUN pacman -Syu --noconfirm 
RUN pacman -S jdk8-openjdk wget --noconfirm; pacman -Scc --noconfirm
COPY setup.sh /
RUN chmod +x setup.sh
RUN ./setup.sh
COPY ./TaxiProducer.tar.gz /
RUN tar -xzvf TaxiProducer.tar.gz
RUN rm TaxiProducer.tar.gz
# zookeeper port
EXPOSE 2181
# kafka port
EXPOSE 9092
