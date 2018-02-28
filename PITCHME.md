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

<img src="cyverse-gis/focus-forum/tree/master/assets/imagery/vertical_large.png" height="200">

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

## Building the best containers for your research

<img src="https://consequenceofsound.files.wordpress.com/2016/04/screen-shot-2016-04-08-at-10-33-51-am.png" width="500">

+++

## Setting up Atmosphere instances as Data Science Workbenches

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

@[1](View option menu for `ez`)
@[2](Install latest version of Docker)
@[3](Install latest version of Singularity)
@[4](Install Anaconda and Jupyter Notebooks w/ Python3 and the R Kernel)

+++

@title[Singularity base Ubuntu]

## <span style="color: #e49436">Docker + RStudio</span>
<br>

```shell
$ ezs
$ singularity pull --name ubuntu14.simg shub://singularityhub/ubuntu
$ singularity run ubuntu14.simg
$ singularity run ubuntu14.simg cat /etc/*release

Done!

```

@[1](Install latest version of Singularity)
@[2](Pull a pre-built Ubuntu image from Singularity Hub)
@[3](Run the Ubuntu image)
@[4](View the version of the image)

+++

@title[Singularity Image from Docker]

## <span style="color: #e49436">Docker + RStudio</span>
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


@[1](install Docker)
@[2](change `sudo` privileges)
@[3](exit and restart terminal window)
@[4](pull the Rocker/Geospatial Rstudio-Server from DockerHub)
@[5](Run the Container in detached mode `-d` on port `-p 8787:8787`)
@[7](Open the Instance's IP address w/ port number in a new browser window)

+++

![Video](https://www.youtube.com/embed/8LSZqWpLbok) 

---

<img src="https://upload.wikimedia.org/wikipedia/en/c/cd/Anaconda_Logo.png" height="200"><img src="http://blog.thedataincubator.com/wp-content/uploads/2017/01/jupyter-logo-300x298.png" height="200">

+++

@title[Anaconda]

## <span style="color: #e49436">Anaconda and Jupyter Notebook</span>
<br>

```shell
$ ezj -3
$ sudo chown $USER:iplant-everyone /home/anaconda3 -R

Done!
```

@[1](Install Anaconda and Jupyter Notebooks w/ Python3 and R Kernel)
@[2](Change ownership of the Anaconda directory so that you can install new kernels)
@[4](Open Jupyter via provided URL w/ token)

---

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

+++?image=assets/imagery/eemt_github.PNG&size=auto 95%

+++?image=assets/imagery/eemt_singularity.png.png&size=auto 95%

---

## Where to get started, if you don't know where to start?

[The Carpentries](https://software-carpentry.org/)

[http://learning.cyverse.org/](http://learning.cyverse.org/)

---

<img src="assets/imagery/cyverse_logo_150px.png" width="150">

### CyVerse is supported by the National Science Foundation under Grants No. DBI-0735191 and DBI-1265383.

<img src="assets/imagery/nsf_logo.png" height="75"> 
<img src="assets/imagery/az.png" height="75"> 
<img src="assets/imagery/tacc.png" height="75"> 
<img src="assets/imagery/cshl.png" height="75"> 
<img src="assets/imagery/uncw.gif" height="75">
