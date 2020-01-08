FROM centos:7

RUN  yum -y install epel-release && yum update -y && \
     yum install -y git git-svn git-email colordiff jq tig bash vim vim-enhanced less openssh hub bash-completion bash-completion-extras wget zip && \
     yum clean all && \
     rm -rf /var/cache/yum

ENV HOME=/home/git
WORKDIR ${HOME}

RUN wget https://raw.github.com/git/git/master/contrib/completion/git-completion.bash && \
    wget https://raw.github.com/git/git/master/contrib/completion/git-prompt.sh

ADD bashrc /home/git/.bashrc

RUN mkdir /projects \
    # Store passwd/group as template files
    && cat /etc/passwd | sed s#root:x.*#root:x:\${USER_ID}:\${GROUP_ID}::\${HOME}:/bin/bash#g > ${HOME}/passwd.template \
    && cat /etc/group | sed s#root:x:0:#root:x:0:0,\${USER_ID}:#g > ${HOME}/group.template \
    # Change permissions to let any arbitrary user
    && for f in "${HOME}" "/etc/passwd" "/etc/group" "/projects"; do \
        echo "Changing permissions on ${f}" && chgrp -R 0 ${f} && \
        chmod -R g+rwX ${f}; \
    done
WORKDIR /projects

ADD entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
CMD tail -f /dev/null


