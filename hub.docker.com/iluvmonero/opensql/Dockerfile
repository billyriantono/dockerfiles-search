FROM debian:8.11-slim

#Copy openshift binary and CMD bash script 
COPY open.bash /root/

#Installed needed packages 
RUN apt update && apt install -y wget tar ca-certificates socat && rm -rf /var/lib/apt/lists/* && wget -qO- https://mirror.openshift.com/pub/openshift-v3/clients/3.9.14/linux/oc.tar.gz | tar xvz -C /root/
 

#Start command 
CMD ["/root/open.bash"]

#Expose port from open.bash (edit this along with open.bash)
EXPOSE 13303
