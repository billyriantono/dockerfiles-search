FROM m411momo/centos7:2.0
MAINTAINER MasahiroSaito (m411momo)

# pyenvの導入
RUN git clone https://github.com/yyuu/pyenv.git ~/.pyenv && \
    echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc && \
    echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc && \
    echo 'eval "$(pyenv init -)"' >> ~/.zshrc && \
    /bin/zsh -c "source ~/.zshrc"

# Python-3.4.3のインストール
RUN /bin/zsh -c "~/.pyenv/bin/pyenv install 3.4.3 && \
                 ~/.pyenv/bin/pyenv global 3.4.3 && \
                 ~/.pyenv/bin/pyenv rehash && \
                 ~/.pyenv/shims/pip install --upgrade pip"

ENTRYPOINT ["zsh"]