FROM konmeo/flask-dev

MAINTAINER konmeo

EXPOSE 8080

WORKDIR /workspace

USER root

RUN install_packages build-essential libssl-dev python tmux && \
    \
    mkdir -p /cloud9 && chown user:user /cloud9 && \
    su user -c "cd /cloud9 && \
        git clone https://github.com/c9/core . && \
        curl -sL https://raw.githubusercontent.com/c9/install/master/link.sh | bash && \
        /cloud9/scripts/install-sdk.sh" && \
    \
    apt-get purge --autoremove -y build-essential libssl-dev && \
    rm -rf /workdir /www /tmp/npm-* /home/user/.c9/tmp/*

RUN pip3 install --no-cache-dir \
        diff-highlight virtualenv

USER user

RUN echo "set -g default-terminal 'screen-256color'" > $HOME/.tmux.conf && \
    sed -i 's/xterm-color/*color/' $HOME/.bashrc && \
    sed -i '$aPATH="$PATH:$HOME/.c9/node/bin:/cloud9/bin"' $HOME/.profile && \
    sed -i 's/127.0.0.1/0.0.0.0/g' /cloud9/configs/standalone.js && \
    sed -i 's/\(.filetree-icon.\)s\(js\)\(:before,\)/\1s\2\3\n\1\2x\3/' \
        /cloud9/plugins/c9.ide.theme.jett/less/overrides.less

RUN mkdir -p $HOME/.c9/python3/bin && \
    virtualenv --no-setuptools --no-pip --no-wheel --python=python3 $HOME/.c9/python3

RUN sed -i -e "s/[, ]pylint[_-]django//" \
           -e "s/\(jedi pylint\)/--user \1==1.9.3/" \
           -e "/upgrade/aln -sf $HOME\/.local/bin\/* $HOME\/.c9\/python3\/bin\/." \
        /cloud9/plugins/c9.ide.language.python/worker/python_linter.js \
        /cloud9/plugins/c9.ide.language.python/server/launch_command.sh && \
    sed -i -e "s_\(.*--untracked-files=no\)_// \1_" \
        /cloud9/plugins/c9.ide.scm/git.js \
        /cloud9/plugins/c9.ide.scm/v1/git.js && \
    sed -i -e "s/250/350/" \
        /cloud9/plugins/c9.ide.scm/v1/detail.js

CMD ["node", "/cloud9/server.js", "--listen","0.0.0.0", "--port","8080", "-w","/workspace"]
