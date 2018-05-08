----

<img src="http://singularity.lbl.gov/images/logo/logo.svg" height="400">

<span style="font-weight: bold; font-size: 150%; color:##FF0000">Introduction to Singularity</span>

+++

#### May 8, 2018
#### Tyson Lee Swetnam
#### CyVerse Science Informatician

+++

### My Contact Info

tswetnam@cyverse.org

github id: [tyson-swetnam](https://github.com/tyson-swetnam) & [cyverse-gis](https://github.com/cyverse-gis)

twitter: tswetnam

---

### Our Roadmap

<span style="color:#FF0000"> The Data Science Workbench </span> <!-- .element: class="fragment" -->

<span style="color:#FF0000"> Why Singularity? </span> <!-- .element: class="fragment" -->

<span style="color:#FF0000"> Installation </span> <!-- .element: class="fragment" -->

<span style="color:#FF0000"> Pulling existing containers </span> <!-- .element: class="fragment" -->

<span style="color:#FF0000"> Building a Singularity file</span> <!-- .element: class="fragment" -->

<span style="color:#FF0000"> Running Singularity </span> <!-- .element: class="fragment" -->

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

## What are some possible pitfalls in designing bespoke software and environments?

+++

<span style="font-weight: bold; font-size: 100%; color:#FF0000">_Dependency Hell_</span> <!-- .element: class="fragment" -->

*different OS + third party software + updates/upgrades + redeployment* = 
 
<img src="https://imgs.xkcd.com/comics/python_environment_2x.png" width="400"> <!-- .element: class="fragment" -->

+++

**Turing Tarpit** - Alan Perlis, 1982 Epigrams on Programming

<img src="https://img00.deviantart.net/58af/i/2012/093/a/c/la_brea_tar_pits_by_felipenn-d4uxy05.jpg" width="400"> <!-- .element: class="fragment" -->

<span style="font-weight: bold; font-size: 80%; color:#FF0000">_Beware of the Turing tar-pit in which **everything is possible** but **nothing of interest is easy**_</span> <!-- .element: class="fragment" -->

+++

## Solution: Containerize your software, run it anywhere. 

+++

## Why Containerize?

<span style="font-weight: bold; font-size: 80%; color:#FF0000"> For the same reasons we talked about Docker yesterday <!-- .element: class="fragment" -->
- Dependencies turn into wicked problems <!-- .element: class="fragment" -->
- Compiling software is sloooowww <!-- .element: class="fragment" -->
- Reproducability is hard across platforms <!-- .element: class="fragment" -->
- Portability <!-- .element: class="fragment" --> **& _Scalability_** <!-- .element: class="fragment" -->

+++

## Singularity Containers for HPC

<img src="http://singularity.lbl.gov/images/logo/logo.svg" width="250">

[Singularity](http://singularity.lbl.gov)

+++

## What makes Singularity different or better than Docker?

- Shares most of the host environment <!-- .element: class="fragment" -->
  - same file system as Linux OS <!-- .element: class="fragment" -->
  - bind extra volumes <!-- .element: class="fragment" -->
- Build your own images <!-- .element: class="fragment" --> 
  - Singularity file <!-- .element: class="fragment" -->
  - Dozens of registries <!-- .element: class="fragment" -->
  - Use existing Docker containers <!-- .element: class="fragment" -->

+++

## Building the "best" containers takes time

<img src="https://consequenceofsound.files.wordpress.com/2016/04/screen-shot-2016-04-08-at-10-33-51-am.png" width="500">

+++

## CyVerse Atmosphere example as a Data Science Workbench

+++

@title[EZ Install]

## <span style="color: #e49436">EZ Install</span>
<br>

```shell
$ ez
$ ezd
$ ezs
$ ezj -R -3
$ ezjh
```

@[1](View option menu for Ansible `ez`)
@[2](Install latest version of Docker)
@[3](Install latest version of Singularity)
@[4](Install Anaconda and Jupyter Notebooks w/ Python3 and the R Kernel)
@[5](Install Jupyter-Hub with CyVerse CAS)

+++

## <span style="color: #e49436">Go with the flow</span>
<br>

<img src="http://singularity.lbl.gov/assets/img/diagram/singularity-2.4-flow.png" height="500">

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

+++

Creating a Singularity container

+++

Write a basic Singularity file

```shell
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

@[1](Select the repository for the container - could be `docker`, `shub`, or `yum`)
@[2](I am selecting to use an image hosted on Hub.Docker - Ubuntu Xenial Xerus 16.04)
@[4](%help is a simple help text)
@[6](%post command runs Bash commands like `apt-get` to install dependencies or programs)
@[9](%environment settings, exporting paths for where to look for the commands)
@[12](%runscript executes the scripts in the container)

+++

@title[Singularity]

## <span style="color: #e49436">Building a Singularity Image</span>
<br>

```shell
$ sudo singularity build --writable cowsay.simg Singularity
$ singularity run cowsay.simg
$ singularity shell cowsay.simg
$ fortune | cowsay | lolcat

Done!
```

@[1](Build a writable image using your Singularity file)
@[2](Run the new image)
@[3](Enter the bash shell inside the container)
@[4](Run the the programs inside the shell)
@[6](Done!)

+++

## Need to run Multi-container jobs?

+++

Scale your research to hundreds and thousands of cores?

<img src="https://raw.githubusercontent.com/cooperative-computing-lab/makeflow-examples/master/banner.png" width="800">

+++

<img src="https://raw.githubusercontent.com/cyverse-gis/focus-forum/master/assets/imagery/eemt_singularity.png.png" width="800">
