FROM centos:6.6

# Install dev tools
RUN yum -y upgrade && yum -y install vim git tar

# Setup vim (pathogen and a few other modules
RUN \
  mkdir -p /root/.vim/autoload /root/.vim/bundle && \
  curl -LSso /root/.vim/autoload/pathogen.vim https://tpo.pe/pathogen.vim && \
  echo 'execute pathogen#infect()' > /root/.vimrc && \
  echo 'syntax on' >> /root/.vimrc && \
  echo 'filetype plugin indent on' >> /root/.vimrc && \
  git clone git://github.com/godlygeek/tabular.git /root/.vim/bundle/tabular && \
  git clone https://github.com/scrooloose/syntastic.git /root/.vim/bundle/syntastic && \
  echo 'set statusline+=%#warningmsg#' >> /root/.vimrc && \
  echo 'set statusline+=%{SyntasticStatuslineFlag()}' >> /root/.vimrc && \
  echo 'set statusline+=%*' >> /root/.vimrc && \
  echo 'let g:syntastic_always_populate_loc_list = 1' >> /root/.vimrc && \
  echo 'let g:syntastic_auto_loc_list = 1' >> /root/.vimrc && \
  echo 'let g:syntastic_check_on_open = 1' >> /root/.vimrc && \
  echo 'let g:syntastic_check_on_wq = 0' >> /root/.vimrc

# Install puppet and puppet dev tools
RUN \
  rpm -ivh http://yum.puppetlabs.com/puppetlabs-release-el-6.noarch.rpm && \
  yum -y upgrade && \
  yum -y install puppet rubygem-puppet-lint rubygem-rake && \
  gem install -v '< 3.0.0' rspec && \
  gem install rspec-puppet && \
  gem install puppetlabs_spec_helper && \
  git clone https://github.com/rodjek/vim-puppet.git /root/.vim/bundle/vim-puppet

WORKDIR /root

CMD ["bash"]
