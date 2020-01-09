FROM jankoppe/arch:latest
LABEL maintainer "Jan Koppe <post@jankoppe.de>"

RUN pacman -Syy --noconfirm awk \
      arm-none-eabi-gcc \
      arm-none-eabi-binutils \
      arm-none-eabi-newlib \
      make \
    && paccache -rk 0 \
    && useradd -m user \
    && usermod -aG uucp user

USER user
VOLUME /code
WORKDIR /code
CMD ["make"]
