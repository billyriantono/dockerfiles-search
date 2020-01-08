FROM archlinux:latest
RUN pacman -Syu --noconfirm && pacman -S --noconfirm wget
RUN wget https://raw.githubusercontent.com/philippe44/AirConnect/master/bin/aircast-x86-64 \
  && chmod +x aircast-x86-64 && mv aircast-x86-64 /bin
ENTRYPOINT ["/bin/aircast-x86-64", "-Z", "-k"]
