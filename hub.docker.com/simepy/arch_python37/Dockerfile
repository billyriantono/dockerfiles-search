FROM archlinux

# create nobody dir
RUN mkdir /home/build
RUN chgrp nobody /home/build
RUN chmod g+ws /home/build
RUN setfacl -m u::rwx,g::rwx /home/build
RUN setfacl -d --set u::rwx,g::rwx,o::- /home/build

RUN pacman -Sy --noconfirm git grep fakeroot binutils xorg-server-xvfb gdb llvm mpdecimal bluez-libs valgrind tk patch file gcc awk make
USER nobody
RUN cd /home/build/ ; git clone https://aur.archlinux.org/python37.git ; cd ./python37 ; makepkg --skippgpcheck

USER root

# clean dependency
RUN pacman -Rns --noconfirm python git grep fakeroot binutils xorg-server-xvfb gdb llvm mpdecimal bluez-libs valgrind tk patch file gcc gawk make

# copy all result of makepkg
RUN cp -r /home/build/python37/pkg/python37/usr/bin/* /usr/bin/
RUN cp -r /home/build/python37/pkg/python37/usr/include/* /usr/include
RUN cp -r /home/build/python37/pkg/python37/usr/lib/* /usr/lib
RUN cp -r /home/build/python37/pkg/python37/usr/share/* /usr/share
RUN ln -s /usr/bin/python3.7 /usr/bin/python

# clean dir
RUN rm -rf /home/build
