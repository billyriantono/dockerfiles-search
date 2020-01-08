FROM m411momo/centos7:2.0
MAINTAINER MasahiroSaito (m411momo)

# rbenvの導入
RUN \
git clone https://github.com/sstephenson/rbenv.git ~/.rbenv && \
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.zshrc && \
echo 'eval "$(rbenv init -)"' >> ~/.zshrc && \
/bin/zsh -c "source ~/.zshrc"

# ruby-buildの導入
RUN \
git clone git://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build && \
~/.rbenv/plugins/ruby-build/install.sh

# Ruby-2.3.1のインストール
RUN /bin/zsh -c "\
~/.rbenv/bin/rbenv install 2.3.1 && \
~/.rbenv/bin/rbenv rehash && \
~/.rbenv/bin/rbenv global 2.3.1 \
~/.rbenv/shims/gem install bundler"

ENTRYPOINT ["zsh"]