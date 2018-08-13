FROM fedora:28
MAINTAINER petter@jebus.nu
LABEL RUN='docker run --rm -it --name vscode -v /home/${USER}:/home/developer -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=${DISPLAY} --security-opt label=type:container_runtime_t pabrahamsson/vscode'
ARG VSCODE_VERSION=1.25.1-1531323952
RUN dnf install -y git zsh tmux libX11-xcb which && \
    dnf install -y https://packages.microsoft.com/yumrepos/vscode/code-${VSCODE_VERSION}.el7.x86_64.rpm && \
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
ENTRYPOINT [ "/bin/tmux" ]