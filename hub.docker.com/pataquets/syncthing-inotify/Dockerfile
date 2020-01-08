FROM golang

RUN \
  go get github.com/syncthing/syncthing-inotify

ENTRYPOINT [ "syncthing-inotify" ]
CMD [ "--help" ]
