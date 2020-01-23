# ARG permet de définir un argument qui peut être surchargé lors du lancement de la commande build.
ARG version=latest
FROM ubuntu:$version

# MAINTAINER est déprécié. Utiliser LABEL maintainer
#MAINTAINER JCD "jcd717@outlook.com"

# Les directives stables (les moins susceptibles d'être modifiées) doivent être au début, afin de permettre au maximum une réutilisation des layers
# Exemple (apt update est nécessaire car généralement les dépôts apt sont vidés. On va d'ailleurs le faire après avoir installé curl): 
# RUN \
#     apt update ; \ 
#     apt install -y curl ; \
#     rm -rf /var/lib/apt/lists/*

# Il est préférable de chainer les instructions en utilisant \ pour éviter la multiplication des couches (chaque commande crée une couche)
LABEL maintainer="JCD <jcd717@outlook.com>" \
      description="test" \
      auteur="bruno dubois"

# Utiliser COPY plutôt que ADD, sauf si c'est un fichier compressé (zip ou tar), car ADD permet de décompresser automatiquement
COPY heartbeat.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh ; \
    echo coucou >test.txt

ARG hbs=3
ENV HEARTBEATSTEP $hbs

# information sur les ports à utiliser (facultatif, c'est de la documentation uniquement)
#EXPOSE 1234/udp 4321/tcp

# ENTRYPOINT est la commande executée au démarrage du container. S'il n'est pas défini, il faut par défaut : /bin/sh -c
ENTRYPOINT ["/entrypoint.sh"]
# CMD sont les arguments de ENTRYPOINT
CMD ["battement"]
# Les crochets et quotes sont inutiles

# Equivalent à : (puisque bin/sh va lancer entrypoint.sh avec comme argument battement)
# CMD /entrypoint.sh battement
