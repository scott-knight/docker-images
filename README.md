# docker-images

This repo contains docker images which load [Ruby 3 (using the slim implimentation)](https://hub.docker.com/_/ruby), [Node (LTS and Current)](https://nodejs.org/en/), and [Yarn Package Manager](https://yarnpkg.com/) to aid in Ruby on Rails development.

To work with docker, you will need to install [Docker Desktop](https://www.docker.com/products/docker-desktop). Once installed and running, you will be able to use the images in this repo.

<br/>

## Debian

This project uses the Debian, slim (bullseye), Ruby image as the base image. Originally, ALPINE was used, but there are less issues using the debian image (for whatever reason).

Here is list of the current Debian image names and versions:

* The next release of Debian is codenamed bookworm — testing — no release date has been set
* Debian 11 (bullseye) — current stable release
* Debian 10 (buster) — current oldstable release
* Debian 9 (stretch) — oldoldstable release, under LTS support
* Debian 8 (jessie) — archived release, under extended LTS support
* Debian 7 (wheezy) — obsolete stable release
* Debian 6.0 (squeeze) — obsolete stable release


<br/>

## Docker Aliases and Functions

This is a list of common docker commands, converted to aliases:

```zsh
# Docker containers
alias dshow="docker ps -a"                 # list all
alias sac='docker stop $(docker ps -a -q)' # stop all
alias dac='docker rm $(docker ps -a -q)'   # delete all

# Stop or delete individual containers, you need the container hash after the call
alias dstop="docker stop"                     # stop single
alias ddel="docker rm -f"                    # delete single

# Docker images
alias imgs="docker images"     # list all
alias dimgs="docker image rm"  # delete
alias daimgs="(docker rmi $(docker images -a -q))" # deletes all images
alias dprune="dac && docker image prune -a -f" # prunes all image content
alias dsprune="docker system prune -a -f" # cleans the system
alias dbp="docker builder prune" # clears the cache

function dclean () {
  docker volume rm $(docker volume ls -q) &&
  sac && dprune && dsprune
}

# Docker-compose
alias dup="docker-compose up"
alias ddown="docker-compose down"
alias ddownv="docker-compose down --volumes"
alias dbuild="dup --build -d"
alias drun="docker-compose run --rm"
```

<br/>

## Ruby 3 Slim - Node 16 (LTS)

This image contains Ruby 3 with the current LTS node. Additionally, it contains updated system files, it updates Ruby Gemsets, Bundler and Rake. It also installs [Oh My ZSH](https://ohmyz.sh/) with the [Spaceship prompt theme](https://github.com/spaceship-prompt/spaceship-prompt).

<br/>

### Building A Ruby 3, Node 16 (LTS) Image

This image is available on [docker hub](https://hub.docker.com/) under the image name `ruby3-node16:latest`.

You can use this repo code to build an image under any name, however, if you would like to build the image with the intended name, run the following:

Change to pwd to `ruby3slim-node16`

```zsh
cd ruby3slim-node16
```

Then run the build command

```zsh
docker image build . -t narcotik33/ruby3-node16:latest
```

<br/>

### The Command-prompt

Once the image is created, you can open the image's ZSH command prompt by running the following:

```zsh
docker container run -it narcotik33/ruby3-node16:latest
```

<br/>

## Building A Ruby 3, Node 17 (CURRENT) Image

This image contains Ruby 3 with Node CURRENT. Additionally, it contains updated system files, it updates Ruby Gemsets, Bundler and Rake. It also installs [Oh My ZSH](https://ohmyz.sh/) with the [Spaceship prompt theme](https://github.com/spaceship-prompt/spaceship-prompt).



This image is available on [docker hub](https://hub.docker.com/) under the image name `narcotik33/ruby3-node17:latest`.

You can use this repo code to build an image under any name, however, if you would like to build the image with the intended name, run the following:

```zsh
docker image build . -t narcotik33/ruby3-node17:latest
```
<br/>

### The Command-prompt

Once the image is created, you can open the image's ZSH command prompt by running the following:

```zsh
docker container run -it narcotik33/ruby3-node17:latest
```
