## Keybase container
([https://keybase.io](https://keybase.io))

### Build
1. `git clone https://github.com/pabrhamsson/dockerfiles`
2. `cd keybase`
3. `docker build -t keybase .`

### Run from build
1. `docker run --rm -it --name keybase -v /home/${USER}:/home/keybase -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=${DISPLAY} --security-opt label=type:container_runtime_t keybase'
2. Once inside the container: `run_keybase`
3. `keybase help`

### Run from prebuilt image
1. `docker run --rm -it --name keybase -v /home/${USER}:/home/keybase -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=${DISPLAY} --security-opt label=type:container_runtime_t quay.io/pabrahamsson/keybase'
2. Once inside the container: `run_keybase`
3. `keybase help`
