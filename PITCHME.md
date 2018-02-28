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

## The Research Object

+++

<span style="font-size: 150%; color:#ffffff">Okay, what is a [Research Object](http://www.researchobject.org/)?</span>

@[1](<span style="font-size: 150%; font-weight: bold; color:#3685E3">broadly, it is a method for identification, aggregation, and exchange of scholarly information</span>)

+++
"_Supporting the publication of *more than just PDFs*, making *data*, *code*, and other resources *first class citizens of scholarship*_"

[Research Objects](http://www.researchobject.org/) have:

- Digital identity: DOI, <!-- .element: class="fragment" --> [ORCID](http://orcid.org/) <!-- .element: class="fragment" -->

- Annotation & Provenance <!-- .element: class="fragment" --> *METADATA!* <!-- .element: class="fragment" -->

Most importantly: they are discoverable & reusable <!-- .element: class="fragment" -->

+++

## Data Science "Workbenches"

+++

## Data scientists need a place to work...

<img src="https://21stcenturyrenaissanceprintmaker.files.wordpress.com/2014/04/nova-reperta-with-letters.png" height="400">

+++

### A data science workbench allows: 

- Work in your preferred environment, languages, and libraries 
- Select the tools you want to use
- Write in a computational notebook  
  - Python, R, C++, Matlab, Spark, etc. 
+++                                             

## Containers

+++

*different OS + third party software + frequent changes and updates + deployment and reproducibility issues* = 
 
<span style="font-weight: bold; font-size: 150%; color:#FF0000">_Dependency Hell_</span> <!-- .element: class="fragment" -->

<img src="https://pbs.twimg.com/media/DB6QcoNVYAA-w6N.jpg" width="350"> <!-- .element: class="fragment" -->

+++

Solution: Containerize your software, run anywhere. 

+++

## Why Containerize?

- Dependencies can be wicked problems <!-- .element: class="fragment" -->
- Compiling software is slow <!-- .element: class="fragment" -->
- Reproducability is hard <!-- .element: class="fragment" -->
- Portability <!-- .element: class="fragment" -->

+++

## Containers for HPC

<img src="http://singularity.lbl.gov/images/logo/logo.svg" width="250">

[Singularity](http://singularity.lbl.gov)

+++

- Shares _most_ of the host environment
  - all mounted volumes
- `root` privileges inside container
  - install your own software on HPC!
- Build your own image or use a Dockerfile

+++

## Demo

+++

## Building the best containers

<img src="https://consequenceofsound.files.wordpress.com/2016/04/screen-shot-2016-04-08-at-10-33-51-am.png" width="500">

+++

## Setting up Atmosphere instances as Data Science Workbench

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

@title[Singularity base Ubuntu]

## <span style="color: #e49436">Pulling Singularity images</span>
<br>

```shell
$ ezs
$ singularity pull --name ubuntu14.simg shub://singularityhub/ubuntu
$ singularity exec ubuntu14.simg
$ singularity exec ubuntu14.simg whoami
$ singulariity exec ubuntu14.simg pwd

Done!

```

@[1](Install latest version of Singularity)
@[2](Pull a pre-built Ubuntu image from Singularity Hub)
@[3](Execute the image with no commands)
@[4](See who the user is inside the container)
@[5](See what the present working directory is inside the container)
@[7](The container has the same filesystem as the machine!)

+++

@title[Singularity Image from Docker]

## <span style="color: #e49436">Docker2Singularity</span>
<br>

```shell
$ ezs
$ singularity pull docker://godlovedc/lolcow
$ singularity run lolcow.img

Done!

```

@[1](Install latest version of Singularity)
@[2](Pull a pre-built Ubuntu image from Docker Hub)
@[3](Run the lolcow image)
@[5](Note, this older version of Singularity uses a `.img` file format)

+++

Creating a Singularity container

+++

Write a Singularity file

```
BootStrap: docker
From: ubuntu:16.04

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

+++
@title[Singularity Image from Docker]

## <span style="color: #e49436">Building a Singularity Image</span>
<br>

```shell
$ ezs
$ $ singularity build --name ubuntu.simg Singularity
$ singularity run lolcow.img

Done!

```

@[1](Install latest version of Singularity)
@[2](Pull a pre-built Ubuntu image from Docker Hub)
@[3](Run the lolcow image)
@[5](Note, this older version of Singularity uses a `.img` file format)

+++

<img src="https://upload.wikimedia.org/wikipedia/en/c/cd/Anaconda_Logo.png" height="200"><img src="http://blog.thedataincubator.com/wp-content/uploads/2017/01/jupyter-logo-300x298.png" height="200">

+++

<img src="assets/imagery/vertical_large.png" height="200"> <img src="https://secure.gravatar.com/avatar/eebe55e8aac8144c9a0e2e1cac5d9057.jpg" height="200">

+++

@title[ArcGIS Jupyter Notebook with Docker]

## <span style="color: #e49436">Docker + Jupyter + ArcPy</span>
<br>

```shell
$ ezd
$ usermod -aG docker $USER
$ exit
$ docker run -it -p 8888:8888 esridocker/arcgis-api-python-notebook

Done!

```

@[1](Install latest version of Docker using `EZ` installation)
@[2](Add yourself to the Docker group on your VM so you can run without `sudo`)
@[3](exit and restart terminal)
@[4](Pull the ArcGIS Jupyter Docker Container)
@[6](The Jupyter notebook should now be running on the localhost - change `localhost` out for the VM's IP address)

---

## Multi-container jobs with Makeflow

+++

How do I scale my research to use hundreds to thousands of computers?
<img src="https://raw.githubusercontent.com/cooperative-computing-lab/makeflow-examples/master/banner.png" width="800">

+++?image=https://github.com/cyverse-gis/focus-forum/blob/master/assets/imagery/eemt_github.PNG?raw=true&size=auto 95%

+++?image=https://github.com/cyverse-gis/focus-forum/blob/master/assets/imagery/eemt_singularity.png.png?raw=true&size=auto 95%
