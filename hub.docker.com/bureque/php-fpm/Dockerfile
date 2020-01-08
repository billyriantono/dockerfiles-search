FROM jprjr/php-fpm
USER root
RUN pacman -Syy --noconfirm --quiet
RUN pacman -S --noconfirm --quiet --needed php-mongo xdebug
RUN paccache -rk0
RUN pacman -Scc --noconfirm
USER http
ENTRYPOINT ["php-fpm", "-F"]
