FROM fedora:29
MAINTAINER petter@jebus.nu
LABEL RUN='docker run -it --rm --name vim.$$ -w $(pwd|sed "s/${USER}/developer/") --cpus 0.3 -m 32 -v /home/${USER}:/home/developer -e TZ=America/New_York --security-opt label=type:container_runtime_t quay.io/pabrahamsson/vim'
RUN dnf install -y git vim-enhanced && \
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
ENTRYPOINT ["vim"]
