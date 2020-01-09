FROM archlinux/base

#update, install jupyter
RUN pacman --noconfirm -Suy && \
    pacman --noconfirm -S jupyter && \
    pacman --noconfirm -Scc

#run jupyter
CMD [ "jupyter-notebook", \
"--ip", "0.0.0.0", "--allow-root",\
"--NotebookApp.token=''", "--NotebookApp.password=''", "--no-browser", "/" ]

#use this port
EXPOSE 8888
