FROM fedora:29
MAINTAINER petter@jebus.nu
LABEL RUN='docker run --rm -it --name rambox -v /home/${USER}:/home/rambox -v /tmp/.X11-unix:/tmp/.X11-unix -v /dev/shm:/dev/shm -e DISPLAY=${DISPLAY} --device /dev/snd -e PULSE_SERVER=unix:${XDG_RUNTIME_DIR}/pulse/native -v ${XDG_RUNTIME_DIR}/pulse/native:${XDG_RUNTIME_DIR}/pulse/native --group-add $(getent group audio | cut -d: -f3) --security-opt label=type:container_runtime_t quay.io/pabrahamsson/rambox'
RUN INSTALL_PKGS="alsa-utils pulseaudio GConf2 gtk3 nss libXScrnSaver" && \
    dnf install -y $INSTALL_PKGS https://github.com/ramboxapp/community-edition/releases/download/0.6.2/Rambox-0.6.2-linux-x86_64.rpm && \
    dnf clean all && \
    export uid=1000 gid=1000 && \
    mkdir -p /home/rambox && \
    echo "rambox:x:${uid}:${gid}:Rambox,,,:/home/rambox:/bin/bash" >> /etc/passwd && \
    echo "rambox:x:${uid}:" >> /etc/group && \
    chown ${uid}:${gid} -R /home/rambox && \
    usermod -a -G audio rambox

USER rambox
ENV HOME /home/rambox
ENV LANG en_US.UTF-8
ENV TERM xterm-256color
WORKDIR /home/rambox
ENTRYPOINT [ "rambox" ]
