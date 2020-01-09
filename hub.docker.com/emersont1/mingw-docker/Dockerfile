FROM archlinux/base

ENV MINGW_TOOLCHAIN_64=/usr/share/mingw/toolchain-x86_64-w64-mingw32.cmake
ENV MINGW_TOOLCHAIN_32=/usr/share/mingw/toolchain-i386-w64-mingw32.cmake

RUN pacman -Syu --noconfirm git cmake base-devel; \
 echo "[multilib]" >> /etc/pacman.conf; \
 echo "Include = /etc/pacman.d/mirrorlist" >> /etc/pacman.conf; \
 echo "[ownstuff]" >> /etc/pacman.conf;\ 
 echo "SigLevel = Optional TrustAll" >> /etc/pacman.conf; \ 
 echo "Server = https://ftp.f3l.de/~martchus/\$repo/os/\$arch" >> /etc/pacman.conf; \
 echo "Server = https://martchus.no-ip.biz/repo/arch/\$repo/os/\$arch" >> /etc/pacman.conf; \
 pacman -Syu --noconfirm git cmake base-devel sdl2 sdl2_image sdl2_ttf sdl2_mixer physfs wine mingw-w64-physfs mingw-w64-cmake mingw-w64-sdl2_ttf mingw-w64-sdl2_image;

