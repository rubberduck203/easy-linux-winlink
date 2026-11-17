# Running Winlink on Linux

This is an attempt to simplify doing Winlink email on Linux operating systems.
It's been tested on Debian and Arch.

Doing Winlink on Linux requires running 3 processes:  
1. `rigctld`
2. `ardopcf`
3. `pat`

It's a pain trying to remember the exact commands and backgrounding them (or running multiple terminals)
and I wanted a way to run a single command and be ready to connect to a gateway. 
I also had a secondary goal of being able to quickly switch between radios.

My initial implementation used [overmind](https://github.com/DarthSim/overmind) and `Procfile`s but I found that not only created duplication,
but there also wasn't a great way to specify that `rigctld` had to be running before `ardopcf` and `pat` depended on both being running.
I've found [process-compose](https://f1bonacc1.github.io/process-compose/) is a much better solution overall.

## Process-Compose

### Installation

#### Arch

`process-compose` is available in the Extra repository.

#### Debian

I already have ~/.local/bin on my PATH

At time of writing v1.124.0 was latest.

```sh
cd ~/Downloads
wget https://github.com/F1bonacc1/process-compose/releases/download/v1.124.0/process-compose_linux_amd64.tar.gz
tar -xzf process-compose_linux_amd64.tar.gz
mv process-compose ~/.local/bin/
```

### Running

There are 3 files in here, a base file, and one for each radio I'm likely to use.
The processes are started in order and once `pat` is healthy, it's opened in the browser.

*X6100*

```sh
process-compose -f process-compose.yml -f process-compose.x6100.yml
```

*IC-7300*

```sh
process-compose -f process-compose.yml -f process-compose.ic7300.yml
```

## Procfile

Legacy method left here because I haven't tested the X6100 with process-compose yet.

```sh
overmind start
```
