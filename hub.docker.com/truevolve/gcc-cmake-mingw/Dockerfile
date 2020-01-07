from archlinux

run pacman --noconfirm -Sy swig base-devel sudo cmake

run mkdir -p /home/developer/ && \
	useradd developer -m && \
        passwd -d developer && \
        printf 'developer ALL=(ALL) ALL\n' | tee -a /etc/sudoers 

copy --chown=developer mingw-w64-binutils-bin mingw-w64-binutils
run sudo -u developer bash -c 'cd mingw-w64-binutils && \
	makepkg --skippgpcheck --noconfirm -si'

copy --chown=developer mingw-w64-headers-bin mingw-w64-headers
run sudo -u developer bash -c 'cd  .. && cd mingw-w64-headers && \
	makepkg --skippgpcheck --noconfirm -si'

copy --chown=developer mingw-w64-crt-bin mingw-w64-crt
run sudo -u developer bash -c 'cd  .. && cd mingw-w64-crt && \
	makepkg --skippgpcheck --noconfirm -si'

copy --chown=developer mingw-w64-winpthreads-bin mingw-w64-winpthreads
run sudo -u developer bash -c 'cd  .. && cd mingw-w64-winpthreads && \
	makepkg --skippgpcheck --noconfirm -si'

copy --chown=developer mingw-w64-gcc-bin mingw-w64-gcc
run sudo -u developer bash -c 'cd  .. && cd mingw-w64-gcc && \
	makepkg --skippgpcheck --noconfirm -si'

USER developer
