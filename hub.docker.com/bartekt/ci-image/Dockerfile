FROM gmacario/build-yocto

RUN sudo apt update
RUN sudo apt install -y smbclient

RUN echo "client min protocol = smb2\nclient max protocol = smb3" | sudo tee -a /etc/samba/smb.conf

