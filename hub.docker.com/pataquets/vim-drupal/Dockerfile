FROM pataquets/vim-vundle

RUN \
  echo "Bundle 'bserem/vim-drupal'" >> ~/.vimrc.bundles && \
  vim +BundleInstall +qall
