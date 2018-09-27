FROM fedora:28
MAINTAINER petter@jebus.nu
LABEL RUN='docker run --rm -it --name keybase -v /home/${USER}:/home/developer -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=${DISPLAY} --security-opt label=type:container_runtime_t pabrahamsson/keybase'
RUN dnf install -y https://prerelease.keybase.io/keybase_amd64.rpm && \
    dnf install -y zsh && \
    dnf clean all && \
    export uid=1000 gid=1000 && \
    mkdir -p /home/developer && \
    echo "developer:x:${uid}:${gid}:Developer,,,:/home/developer:/bin/zsh" >> /etc/passwd && \
    echo "developer:x:${uid}:" >> /etc/group && \
    chown ${uid}:${gid} -R /home/developer

USER developer
ENV HOME /home/developer
ENV LANG en_US.UTF-8
ENV TERM xterm-256color
WORKDIR /home/developer
CMD ["/bin/zsh"]
RUN run_keybase
