FROM rundeck/rundeck:SNAPSHOT

USER root

RUN apt-get update && \
    apt-get -y install apt-transport-https curl && \
    apt-get -y install jq

# add cli tool debian repo
RUN echo "deb https://dl.bintray.com/rundeck/rundeck-deb /" | sudo tee -a /etc/apt/sources.list
RUN curl "https://bintray.com/user/downloadSubjectPublicKey?username=bintray" > /tmp/bintray.gpg.key
RUN apt-key add - < /tmp/bintray.gpg.key
RUN apt-get -y update
RUN apt-get -y install rundeck-cli

# RUNDECK
## RUNDECK setup env

ENV USERNAME=rundeck \
    USER=rundeck \
    HOME=/home/rundeck \
    LOGNAME=$USERNAME \
    TERM=xterm-256color


WORKDIR $HOME
USER rundeck

COPY --chown=rundeck:rundeck remco /etc/remco

RUN wget https://github.com/rundeck-plugins/vault-storage/releases/download/1.1.0/vault-storage-1.1.0.jar -P ./libext
#COPY /home/rundeck/vault-storage-1.1.0.jar ./libext

VOLUME ["/home/rundeck/server/data"]

EXPOSE 4440
ENTRYPOINT [ "docker-lib/entry.sh" ]