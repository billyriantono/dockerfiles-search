FROM archlinux

RUN pacman -Sy --noconfirm --noprogressbar reflector
RUN reflector --verbose --age 12 --protocol https --sort rate --save /etc/pacman.d/mirrorlist
RUN pacman -Syyu --noconfirm --noprogressbar \
	git clang python python-pip flake8 rustup wget fd hyperfine ripgrep openssh
RUN rustup install nightly && rustup default nightly
ENV PATH=~/.cargo/bin:$PATH
RUN pip install cpplint flake8
RUN curl -L -o /usr/bin/bazel https://github.com/bazelbuild/bazel/releases/download/2.0.0/bazel-2.0.0-linux-x86_64 && chmod a+x /usr/bin/bazel

# locale
ENV LANG=en_US.UTF-8
RUN echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen && locale-gen

