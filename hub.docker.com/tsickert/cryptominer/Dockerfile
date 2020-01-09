# region header
# [Project page](https://torben.website/proxy)

# Copyright Torben Sickert (info["~at~"]torben.website) 16.12.2012

# License
# -------

# This library written by Torben Sickert stand under a creative commons naming
# 3.0 unported license.
# See https://creativecommons.org/licenses/by/3.0/deed.de
# endregion
# region create image commands
# Run the following command in the directory where this file lives to build a
# new docker image:
# - podman pull docker.pkg.github.com/thaibault/containerbase/base:latest && podman build --file Dockerfile --no-cache --tag docker.pkg.github.com/thaibault/cryptominer/cryptominer
# - docker pull tsickert/base && docker build --no-cache --tag tsickert/cryptominer:latest .
# - podman push docker.pkg.github.com/thaibault/cryptominer/cryptominer:latest --creds "thaibault:$(cat "${ILU_CONFIGURATION_PATH}web/github/masterToken.txt")"
# - docker push tsickert/cryptominer
# endregion
# region start container commands
# Run the following command in the directory where this file lives to start:
# - podman pod rm --force cryptominer_pod; podman play kube kubernetes/full.yaml
# - docker rm --force cryptominer; docker-compose --file docker/full.yaml up
# endregion
            # region configuration
#FROM        docker.pkg.github.com/thaibault/containerbase/base:latest
FROM        tsickert/base
LABEL       maintainer="Torben Sickert <info@torben.website>"
LABEL       Description="cryptoMiner" Vendor="thaibault products" Version="1.0"
EXPOSE      8080
            ## region application specific configuration
ENV         ADDRESS '47AnUWXMN6NPZajLM2dF2W9uwcQuhq9Gghhoit7R2w4fRjLYpgqN7PQ7bBJKPKuF5WQzZXu5cbFcf6BVyvguSweG33khvFD'
ENV         ALGORYTHMUS 'randomX'
ENV         LOGIN_PASSWORD 'info@torben.website'
ENV         NAME "$(hostname)"
ENV         PORT 5555
ENV         RIGID 1
ENV         URL "stratum+tcp://pool.supportxmr.com:$PORT"
ENV         INFO_COMMAND 'echo Start with algorithm $ALGORYTHMUS identifier ${NAME}:${LOGIN_PASSWORD} on url $URL via user $ADDRESS'
ENV         XMR_STAK_COMMAND '${INFO_COMMAND}; xmr-stak --currency "$ALGORYTHMUS" --httpd 8080 --pass "${NAME}:${LOGIN_PASSWORD}" --rigid "$RIGID" --url "$URL" --user "$ADDRESS"'
ENV         XMR_RIG_COMMAND '${INFO_COMMAND}; xmrig --keepalive --pass "${NAME}:${LOGIN_PASSWORD}" --url "$URL" --user "$ADDRESS"'
ENV         COMMAND '$XMR_RIG_COMMAND'
            ## endregion
ENV         PRIVATE_SSH_KEY '-----BEGIN RSA PRIVATE KEY-----\nMIIEogIBAAKCAQEAo3dh12LT/NWx+0bPDyZDuZc6EtlUz5z4On+cFq7nIj4P4fQf\njMjPuYuH6P6szZHyPiV487GKahmX+uFgo+dByPiH1ULY+xDE/cNaD1p+Xg5qjw7m\nfjfklI3eu8M0wYh1nIhIycK2N8b1OlJ753cFC3WAdg3CvlRHh5QZV6hEOhcxuEZU\nzk5TGWtBGXVtlnMGZXKsIBMnsRmJgftG4SdU7V2O+1ZiDi4ePmzTUUhwQjidyDbT\ngaIiXJPNQVpQ/eakfXRDLhcUEE9X7pWtwVTymX7ECpunjd+CWpfDOg8liNM7m6zd\nzEGbgW/eNFZ68g+vCgM+hC08GmM8agSTzIox/wIDAQABAoIBAGP/+F7nGoAlyofJ\nvYmrAutaVDCLu5J2mHRQ9I/713HfPaAg09wwTMNZVH94rQXlLqhODDwodGCL36me\njpw2MMxdHduc1Vhh3eDPzRxvY7buYsm5d8/nKXKnh4ad2Hw8mpZz2PN0pjxg/kv7\ngckLyo5EB54wtN3yeP+73fT9/x75bv9uBbAUYhcooWGiFtDU9KGhHHL56FO8LMfk\nwDOk29/zEUsqpsursWWADXvjRXmuL5CKSgR+5S6I3Ezt2gdYd+/97xgveWBGdTmm\n4teMAPxUlxDcZaj9q/hjohBTCvzUwfvEAiNWqKC15Z4GIn5DU66dR2R+nJn9Ar1h\nNHrAoyECgYEA1EOUTd4bI0UnxxW65me8j934WEv7xt7diH8Tl5nXf9sag4aTmKfW\nQ/O5zvY2RcILbebVKqPzDjSnKhvbG0vu1SQY+e7p9Mg4HakjaX/E2ufLPvIvHpbA\negy/yNMas3ihO6IVVjikuxiKq0hoxVyst/qbMsLI4gx1UdX7fPvPz+0CgYEAxSXX\n0i6ilXx8iEcVlGtziRtTNeTBNNqvcncVGK9PHsc6ewGLbSFDg9pB5rpv61TCL8/Z\nLSbhGnScmTMSNNGzKN5C5moEoRwB8TJxZSNAtPmdiGGGxnw/Gyp4uBjrVOvnHtnb\nYWwR4Z09H2IO9fHpMo8Uvjn1n5lzcPyTgsdL1BsCgYB2ZIMxs3Kbh5UaPAqVPMM1\n028TgL4cPG6AFbEN2+cRD1qIheWJPgQKvsSipT28RvEtCZVYRT3qbH/YwtTBMucx\nxwKPVSz1NT/ne1GfJH7eQm9g2qBhhWAyMy49i1HXTK9RnaQdBVcMbDHcO3UEsB4+\nN++crnxxaNV/IcU1/xX4OQKBgCG3Pxmq8BMwnvuPbJldZvzjt29YF9K6M5cX1nvK\nP3W8DLxMn1OihLFf+jVDXTCZ5jvXCAU4yPaFSuLIYSy3UDSFDlvpdbE34P0m602o\nocBRkCdqxmnbhc9XjB2v5U84qOYVy/b1THmRMorTckuNe5wx7BI8R01sKNoB2Bhd\njRJRAoGATNt/Ia602EaeXVF7WBEzmghjf385HSI4u1G45cux/R5ct4SMBbYkdOdA\n6M1h9V90RuPRYxcJu5SlFGdV+TU8ZMHHtwm9yTWrrNe+XReX/cd8wT08MzjeD3WJ\nfGdHCkgzb7PQRbNMGsNManoDWBVVYGRsxvTOZ1EHLYXhFeNSqpk=\n-----END RSA PRIVATE KEY-----'
ENV         PUBLIC_SSH_KEY 'ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCjd2HXYtP81bH7Rs8PJkO5lzoS2VTPnPg6f5wWruciPg/h9B+MyM+5i4fo/qzNkfI+JXjzsYpqGZf64WCj50HI+IfVQtj7EMT9w1oPWn5eDmqPDuZ+N+SUjd67wzTBiHWciEjJwrY3xvU6UnvndwULdYB2DcK+VEeHlBlXqEQ6FzG4RlTOTlMZa0EZdW2WcwZlcqwgEyexGYmB+0bhJ1TtXY77VmIOLh4+bNNRSHBCOJ3INtOBoiJck81BWlD95qR9dEMuFxQQT1fula3BVPKZfsQKm6eN34Jal8M6DyWI0zubrN3MQZuBb940VnryD68KAz6ELTwaYzxqBJPMijH/ dockerBase'
ENV         KNOWN_HOSTS 'github.com,192.30.253.112 ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAq2A7hRGmdnm9tUDbO9IDSwBK6TbQa+PXYPCPy6rbTrTtw7PHkccKrpp0yVhp5HdEIcKr6pLlVDBfOLX9QUsyCOV0wzfjIJNlGEYsdlLJizHhbn2mUjvSAHQqZETYP81eFzLQNnPHt4EVVUh7VfDESU84KezmD5QlWpXLmvU31/yMf+Se8xhHTvKSCZIFImWwoG6mbUoWf9nzpIoaSjB+weqqUUmpaaasXVal72J+UX2B+2RPW3RcT0eOzQgqlJL3RKrTJvdsjE3JEAvGq3lGHSZXy28G3skua2SmVi/w4yCE6gbODqnTWlg7+wC604ydGXA8VJiS5ap43JXiUFFAaQ=='
ENV         REPOSITORY_URL 'git@github.com:thaibault/cryptoMiner.git'
USER        root
            # endregion
            # region install needed packages
            # NOTE: For grafical interface support include "cuda" here.
RUN         pacman \
                --needed \
                --noconfirm \
                --sync \
                cmake \
                hwloc \
                libmicrohttpd \
                ocl-icd \
                opencl-headers \
                openssl && \
            # tidy up
            rm /var/cache/* --recursive --force
            # endregion
RUN         configure-user
RUN         retrieve-application
            # region configure and integrate current application
            ## region xmrstak
RUN         pushd xmr-stak && \
            sed \
                --in-place \
                's/\(fDevDonationLevel = \).*\(;\)/\10.0\2/g' \
                xmrstak/donate-level.hpp && \
            CC=/bin/gcc CXX=/bin/g++ cmake -DCUDA_ENABLE=OFF . && \
            make && \
            cp bin/xmr-stak /usr/bin/ && \
            [ -f bin/libxmrstak_cuda_backend.so ] && \
            cp bin/libxmrstak_cuda_backend.so /usr/lib || \
            cp bin/libxmrstak_opencl_backend.so /usr/lib; \
            popd
            ## endregion
            ## region xmrig
RUN         pushd xmrig && \
            mkdir build && \
            cmake -DCMAKE_BUILD_TYPE=Release . && \
            make && \
            cp xmrig /usr/bin/ && \
            popd
            ## endregion
            # endregion
# region modline
# vim: set tabstop=4 shiftwidth=4 expandtab filetype=dockerfile:
# vim: foldmethod=marker foldmarker=region,endregion:
# endregion
