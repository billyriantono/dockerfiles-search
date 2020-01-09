FROM    base/archlinux:latest

RUN pacman -Syu --noconfirm &&\
    pacman -S --noconfirm texlive-{core,bin,bibtexextra,fontsextra,formatsextra,games,humanities,langchinese,langcyrillic,langextra,langgreek,langjapanese,langkorean,latexextra,music,pictures,pstricks,publishers,science} &&\
    pacman -S --noconfirm biber ghostscript ruby perl-tk psutils dialog ed poppler-data &&\
    pacman -S --noconfirm python python-{pandas,matplotlib,numpy,scipy,sympy} &&\
    pacman -Scc --noconfirm
    
CMD ["/bin/bash", "echo", ""Hello, I am Texlive on Archlinux!""]
