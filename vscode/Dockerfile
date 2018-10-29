FROM fedora:29
MAINTAINER petter@jebus.nu
LABEL RUN='docker run --rm -it --name vscode -v /home/${USER}:/home/developer -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=${DISPLAY} --security-opt label=type:container_runtime_t quay.io/pabrahamsson/vscode'
RUN rpm --import https://packages.microsoft.com/keys/microsoft.asc && \
    echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo && \
    dnf install -y git libX11-xcb which code && \
    dnf upgrade -y && \
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
ENTRYPOINT ["code"]
