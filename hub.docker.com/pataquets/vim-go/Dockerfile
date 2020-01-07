FROM pataquets/vim-vundle

ADD .vimrc.bundles /root/
RUN \
  vim "+set nomore" "+BundleInstall!" "+BundleClean" "+qall"

ENTRYPOINT [ "vim" ]
CMD [ "/src/" ]
