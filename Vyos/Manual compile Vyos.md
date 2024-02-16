# Build via docker

```
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

## Build from source
The container can also be built directly from source:

```
#### For VyOS 1.2 (crux)
$ git clone -b crux --single-branch https://github.com/vyos/vyos-build
#### For VyOS 1.3 (equuleus)
$ git clone -b equuleus --single-branch https://github.com/vyos/vyos-build
#### For VyOS 1.4 (sagitta)
$ git clone -b sagitta --single-branch https://github.com/vyos/vyos-build
#### For VyOS 1.5 (circinus,current)
$ git clone -b current --single-branch https://github.com/vyos/vyos-build

$ cd vyos-build
$ docker build -t vyos/vyos-build:crux docker           # For VyOS 1.2
$ docker build -t vyos/vyos-build:equuleus docker       # For VyOS 1.3
$ docker build -t vyos/vyos-build:sagitta docker        # For VyOS 1.4
$ docker build -t vyos/vyos-build:current docker        # For VyOS 1.5 rolling release
```


## Build ISO
Now as you are aware of the prerequisites we can continue and build our own ISO from source. For this we have to fetch the latest source code from GitHub. Please note as this will differ for both current and crux.

```
#### For VyOS 1.2 (crux)
$ git clone -b crux --single-branch https://github.com/vyos/vyos-build

#### For VyOS 1.3 (equuleus)
$ git clone -b equuleus --single-branch https://github.com/vyos/vyos-build

#### For VyOS 1.4 (sagitta)
$ git clone -b sagitta --single-branch https://github.com/vyos/vyos-build

#### For VyOS 1.5 (circinus,current)
$ git clone -b current --single-branch https://github.com/vyos/vyos-build
```

Now a fresh build of the VyOS ISO can begin. Change directory to the vyos-build directory and run:

```
$ cd vyos-build
#### For VyOS 1.2 (crux)
$ docker run --rm -it --privileged -v $(pwd):/vyos -w /vyos vyos/vyos-build:crux bash

#### For VyOS 1.3 (equuleus)
$ docker run --rm -it --privileged -v $(pwd):/vyos -w /vyos vyos/vyos-build:equuleus bash

#### For VyOS 1.4 (sagitta)
$ docker run --rm -it --privileged -v $(pwd):/vyos -w /vyos vyos/vyos-build:sagitta bash

#### For VyOS 1.5 (current)
$ docker run --rm -it --privileged -v $(pwd):/vyos -w /vyos vyos/vyos-build:current bash
```
