FROM phusion/baseimage:0.11

CMD ["/sbin/my_init"]

SHELL ["/bin/bash", "-c"]

RUN true \
    && echo -e "set encoding=utf-8\nset fileencoding=utf-8\nset fileencodings=ucs-bom,utf-8,cp936,gb18030,big5,euc-jp,euc-kr,latin1\n\nnoremap <space> :\n\nnoremap <space>e :e<CR>\nnoremap <space>eg :e<CR>G\nnoremap <space>egz :e<CR>GzR\n\nnoremap <space>bp :bp<CR>\nnoremap <space>bn :bn<CR>\nnoremap <space>bd :bd<CR>\nnoremap <space>bb :e #<CR>\n\nnoremap <space>w :w<CR>\nnoremap <space>wq :wq<CR>\nnoremap <space>wqa :wqa<CR>\n\nnoremap <space>cp :cp<CR>\nnoremap <space>cn :cn<CR>\nnoremap <space>cw :cw<CR>\n\nnoremap <space>q :q<CR>\nnoremap <space>qa :qa<CR>\n" >> /etc/vim/vimrc \
    && sed -i 's/http:\/\/archive\.ubuntu\.com\/ubuntu\//http:\/\/mirrors\.aliyun\.com\/ubuntu\//g' /etc/apt/sources.list \
    && sed -i 's/http:\/\/security\.ubuntu\.com\/ubuntu\//http:\/\/mirrors\.aliyun\.com\/ubuntu\//g' /etc/apt/sources.list \
    && export DEBIAN_FRONTEND=noninteractive \
    && apt-get update \
    && apt-get install -y -q --no-install-recommends \
    wget bzip2 rsync htop sysstat strace lsof net-tools gettext-base bash-completion \
    && rm -f /etc/service/sshd/down && /etc/my_init.d/00_regen_ssh_host_keys.sh && /usr/sbin/enable_insecure_key \
    && echo -e "-----BEGIN RSA PRIVATE KEY-----\nMIIEpQIBAAKCAQEA1ZswRub+3DvSEnBiyM5YRpRzRYV88vO1X2j867u6pyCHUNXv\nRRCr7ahMLPIVYsZwlHb4sF+Zb3DJOBH+E265o93chdMxbWG44k0spf10JRevA0JX\nNrEwHR8vesCR74e5MuddbSic88lsEqnnn+Fo3lStvE6nBp6tbqdEu7GhTtHSYejn\nwwINnA5ocsHkd1YE9L2Scqw1e4bXveTAQnSvhqe33QshGXFpt0tQwRWngah887f2\nP54wFSm2C/UyFT7pvIjINKzIi4vUoXz/nU+V7neTmt3XDdjloYg3ycOaX4RSVneO\nHCf7hkcEKbzbPzzSrGAAYYC5UzFB+ImsIbtV2wIDAQABAoIBAQCjROxgtX2Gft7y\nIx8Ol9IXmK6HLCI2XZt7ovb3hFWGGzHy0qMBql2P2Tzoed1o038Hq+woe9n+uTnE\ndtQ6rD6PByzgyW2VSsWTjCOdeJ5HH9Qw7ItXDZZWHBkhfYHOkXI4e2oI3qshGAtY\nNLALn7KVhioJriCyyaSM2KOLx5khcY+EJ1inQfwQJKqPGsdKc72liz07T8ifRj+m\nNLKtwrxlK3IXYfIdgLp/1pCKdrC80DhprMsD4xvNgq4pCR9jd4FoqM9t/Up5ppTm\n+p6A/bDwdIPh6cFFeyMP+G3+bTlW1Gg7RLoNCc6qh53WWVgEOQqdLHcQ8Ge4RLmb\nwLUmnRuRAoGBAPfXYfjpPZi8rPIQpux13Bs7xaS1/Fa9WqrEfrPptFdUVHeFCGY8\nqOUVewPviHdbs0nB71Ynk9/e96agFYijQdqTQzVnpYI4i8GiGk5gPMiB2UYeJ/HZ\nmIB3jtWyf6Z/GO0hJ1a6mX0XD3zJGNqFaiwqaYgdO1Fwh9gcH3O2lHyjAoGBANyj\nTGDBYHpxPu6uKcGreLd0SgO61PEj7aOSNfrBB2PK83A+zjZCFZRIWqjfrkxGG6+a\n2WuHbEHuCGvu2V5juHYxbAD/38iV/lQl/2xyvN1eR/baE3US06qn6idxjnmeNZDy\nDelAx1RGuEvLX1TNAzDTxBwYyzH3W2RpKAUAD11pAoGAN38YJhd8Pn5JL68A4cQG\ndGau/BHwHjAqZEC5qmmzgzaT72tvlQ0SOLHVqOzzHt7+x45QnHciSqfvxnTkPYNp\nFJuTGhtKWV12FfbJczFjivZgg63u/d3eoy2iY0GkCdE98KNS3r3L7tHCGwwgr5Xe\nT2Nz3BHHnZXYJVEuzcddeocCgYEAnhDjPAHtw2p0Inxlb9kPb6aBC/ECcwtBSUkL\nIOy/BZA1HPnxs89eNFAtmwQ8k2o6lXDDSJTJSuZj5CdGVKfuU8aOUJz/Tm2eudxL\nA/+jLJhJyCBthhcJyx3m04E4CAr+5ytyKeP9qXPMvoghcNg66/UabuKYV+CU+feX\n8xUa7NkCgYEAlX8HGvWMmiG+ZRFB//3Loy87bBxGlN0pUtCEScabZxdB2HkI9Vp7\nYr67QIZ3y7T88Mhkwam54JCjiV+3TZbSyRMOjkqf7UhTCZC6hHNqdUnlpv4bJWeW\ni5Eun8ltYxBnemNc2QGxA4r+KCspi+pRvWNGzL3PFVBGXiLsmOMul78=\n-----END RSA PRIVATE KEY-----" > /root/.ssh/id_rsa && chmod 600 /root/.ssh/id_rsa \
    && cp /root/.ssh/authorized_keys /root/.ssh/id_rsa.pub && chmod 600 /root/.ssh/id_rsa.pub \
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
