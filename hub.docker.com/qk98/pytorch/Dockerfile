FROM pytorch/pytorch:1.1.0-cuda10.0-cudnn7.5-runtime
RUN echo "PS1='\n${debian_chroot:+($debian_chroot)}\[\033[01;35;40m\]\u@\h\[\033[00;40m\]:\[\033[01;34;40m\] \w\[\033[01;32;40m\]\n $ '" >> ~/.bashrc \
 && echo 'set completion-ignore-case On' >> /etc/inputrc

