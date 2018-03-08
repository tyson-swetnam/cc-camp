---?image=assets/imagery/merged.png&size=cover
<span style="font-weight: bold; font-size: 150%; color:#FFFF00">Introduction to Singularity</span>

+++

#### March 8, 2018
#### Tyson Lee Swetnam
#### CyVerse Science Informatician

+++

### Contact Info

tswetnam@cyverse.org

github: [tyson-swetnam](https://github.com/tyson-swetnam) [cyverse-gis](https://github.com/cyverse-gis)

twitter: tswetnam

---

### Our Roadmap


<span style="color:#ffffff"> Why use Singularity? </span> <!-- .element: class="fragment" -->

<span style="color:#ffffff"> Installation of Singularity </span> <!-- .element: class="fragment" -->

<span style="color:#ffffff"> Pulling Containers </span> <!-- .element: class="fragment" -->

<span style="color:#ffffff"> Building a Singularity container </span> <!-- .element: class="fragment" -->

<span style="color:#ffffff"> Running Singularity </span> <!-- .element: class="fragment" -->

---

+++

## Data Science "Workbenches"

+++

## Data scientists need a place to work...

<img src="https://21stcenturyrenaissanceprintmaker.files.wordpress.com/2014/04/nova-reperta-with-letters.png" height="400">

+++

### A data science workbench allows: 

- Favored environment, languages, and libraries 
- Tools you want to use
- Computational notebooks 
  - Python, R, C++, Matlab, Spark, etc. 
  
+++                                             

*different OS + third party software + frequent changes and updates + deployment and reproducibility issues* = 
 
<span style="font-weight: bold; font-size: 150%; color:#FF0000">_Dependency Hell_</span> <!-- .element: class="fragment" -->

<img src="https://pbs.twimg.com/media/DB6QcoNVYAA-w6N.jpg" width="350"> <!-- .element: class="fragment" -->

+++

## Solution: Containerize your software, run anywhere. 

+++

## Why Containerize?

- Dependencies can be wicked problems <!-- .element: class="fragment" -->
- Compiling software is slow <!-- .element: class="fragment" -->
- Reproducability is hard <!-- .element: class="fragment" -->
- Portability <!-- .element: class="fragment" -->

+++

*Turing Tarpit - Alan Perlis 1982 Epigrams on Programming*

<img src="https://img00.deviantart.net/58af/i/2012/093/a/c/la_brea_tar_pits_by_felipenn-d4uxy05.jpg" width="450"> <!-- .element: class="fragment" -->

<span style="font-weight: bold; font-size: 80%; color:#FF0000">_Beware of the Turing tar-pit in which everything is possible but nothing of interest is easy._</span> <!-- .element: class="fragment" -->

+++

## Containers for HPC

<img src="http://singularity.lbl.gov/images/logo/logo.svg" width="250">

[Singularity](http://singularity.lbl.gov)

+++

- Shares _most_ of the host environment
  - same file system as Linux OS
  - bind extra volumes
- Build your own images 
  - Singularity file
  - Dozens of registries
  - existing Docker containers 

+++

## Building the best containers

<img src="https://consequenceofsound.files.wordpress.com/2016/04/screen-shot-2016-04-08-at-10-33-51-am.png" width="500">

+++

## Atmosphere / Jetstream instances as Data Science Workbenches

+++

- Create a new instance in Atmosphere / Jetstream

- If you are planning to "image" the instance, select the smallest functional size.

  - Install new software into `/opt` `/srv`

+++

@title[EZ Install]

## <span style="color: #e49436">EZ Install</span>
<br>

```shell
$ ez
$ ezd
$ ezs
$ ezj -R -3
```

@[1](View option menu for Ansible `ez`)
@[2](Install latest version of Docker)
@[3](Install latest version of Singularity)
@[4](Install Anaconda and Jupyter Notebooks w/ Python3 and the R Kernel)

+++

@title[Singularity Hub]

## <span style="color: #e49436">Pulling Singularity images</span>
<br>

```shell
$ ezs
$ singularity pull shub://singularity/ubuntu:latest
$ singularity pull --name ubuntu14.simg shub://singularityhub/ubuntu

Done!

```

@[1](Install latest version of Singularity)
@[2](Pull a pre-built Ubuntu image from Singularity Hub)
@[3](Pulls a pre-built image and renames it)
@[5](Image is now on your localhost)

+++

@title[Singularity Hub]

## <span style="color: #e49436">Pulling Singularity images</span>
<br>

```shell
$ whoami
$ cat /etc/*release
$ singularity exec ubuntu14.simg whoami
$ singularity exec ubuntu14.simg cat /etc/*release

Done!

```

@[1](View the user profile)
@[2](View OS release)
@[3](View the user profile inside the container)
@[4](View OS release of the container)

+++

@title[Singularity Image from Docker]

## <span style="color: #e49436">Docker Images</span>
<br>

```shell
$ singularity pull docker://godlovedc/lolcow
$ singularity run lolcow.simg

Done!

```

@[1](Pull a pre-built Ubuntu image from Docker Hub)
@[2](Run the lolcow image)
@[5](Note, this older version of Singularity uses a `.img` file format)

+++

Creating a Singularity container

+++

Write a basic Singularity file

```
BootStrap: docker
From: ubuntu:16.04

%help
  "This container tells a joke" 
  
%post
  apt-get -y update
  apt-get -y install fortune cowsay lolcat

%environment
  export LC_ALL=C
  export PATH=/usr/games:$PATH

%runscript
  fortune | cowsay | lolcat
```

@[1](Here I am using the BootStrap command - note this command has been depreciated in the CLI)
@[2](I am selecting to use an image hosted on DockerHub - Ubuntu Xenial Xerus 16.04)
@[4](The %post command runs Bash commands like `apt-get` to install dependencies or programs)
@[5](Update!)
@[6](install jokes)
@[8](The %environment settings, exporting paths for where to look for the commands)
@[12](The %runscript executes the scripts in the container)
@[13](run the three jokes at the same time using the pipe `|`)

+++

@title[Singularity]

## <span style="color: #e49436">Building a Singularity Image</span>
<br>

```shell
$ sudo singularity build --writable ubuntu.simg Singularity
$ sudo singularity shell ubuntu.simg
$ fortune | cowsay | lolcat
$

Done!

```

@[1](Build a writable image using your Singularity file)
@[2](Enter the bash shell inside the container)
@[3](Run the lolcow image)
@[5](Done!)

+++

@title[Singularity]

## <span style="color: #e49436">Building a Singularity Image</span>
<br>

```shell
$ ezs
$ singularity build --name ubuntu.simg Singularity
$ singularity run lolcow.img

Done!

```

@[1](Install latest version of Singularity)
@[2](Pull a pre-built Ubuntu image from Docker Hub)
@[3](Run the lolcow image)
@[5](Note, this older version of Singularity uses a `.img` file format)


+++

## Multi-container jobs

+++

How do I scale my research to use hundreds to thousands of computers?
<img src="https://raw.githubusercontent.com/cooperative-computing-lab/makeflow-examples/master/banner.png" width="800">

+++?image=https://github.com/cyverse-gis/focus-forum/blob/master/assets/imagery/eemt_github.PNG?raw=true&size=auto 95%

+++?image=https://github.com/cyverse-gis/focus-forum/blob/master/assets/imagery/eemt_singularity.png.png?raw=true&size=auto 95%
