FROM centos/systemd                                                                                     
ENV container docker                                                                                    
RUN yum install -y epel-release && \                                                                    
    yum install -y iproute initscripts && \                                                             
    mkdir -p /var/tank/ansible-tower-setup && \                                                         
    mkdir -p /var/log/tower                                                                             
ADD  http://releases.ansible.com/ansible-tower/setup/ansible-tower-setup-latest.tar.gz /var/tank        
WORKDIR /var/tank                                                                                       
RUN tar xvf ansible-tower-setup-latest.tar.gz -C /var/tank/ansible-tower-setup --strip-components=1 \   
    && rm -f /var/tank/ansible-tower-setup-latest.tar.gz \                                              
EXPOSE 80                                                                                               
EXPOSE 443                                                                                              
COPY ./inventory /var/tank/ansible-tower-setup/inventory                                         
                                                                                                        
