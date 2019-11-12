<!--
    $size: 16:9
    $theme: default
    page_number: true
    footer: Supercomputing 2019
-->
<!-- *footer: -->
<!-- *page_number: -->
<link rel="stylesheet" type="text/css" href="css/ecp.css"></link>

![bg](img/background_sc19.png)
# Cinema Tutorial November 2019
## Supercomputing Tutorial, Denver, CO

David Rogers, James Ahrens, Terry Turton, Soumya Dutta,
Divya Banesh, Roxana Bujack, Ethan Stam


---
![bg](img/background_sc19.png)

# Tutorial Goals

<!-- TODO update image to montage -->
<img src="img/montage.png" width="35%" align="right" valign="top">

- **Introduce Cinema**
	- Inspect a simple Cinema database
- **Cinema Algorithms**
    - Run command line algorithms on a Cinema database
- **Create a Cinema Database with ParaView**
	- Load data and export with ParaView
- **Further Information**
	- Pointers to more tutorials and instructions

---
# Where Does Cinema Fit into in-situ Analysis
<img src="img/ECP_DAV_diagram.png" width="90%" align="center">

---
![bg](img/background_sc19.png)
# ECP Calls for the use of in-situ workflows
<img src="img/ECP_DAV_diagram.png" width="20%" valign="bottom" align="right">

- Algorithms produce artifacts in permanent storage
- Those artifacts:
    - Will be very different from our current artifacts in permanent storage
    - Will need different application support to explore them
    - Will themselves be inputs to analysis workflows
- Cinema is a project dedicated to these requirements

<br></br>
## Today we will work with basic examples

---
![bg](img/background_sc19.png)
# Algorithm-based data extraction is a change ...
<img src="img/extracts.png" width="100%" align="right">

---
![bg](img/background_sc19.png)
# What is Cinema?
<img src="img/ecosystem.png" width="50%" align="right">

Cinema is and ecosystem consisting of:

- database specification,
- database writers
- database viewers
- algorithms

Designed to help explore extreme scale data.

---
![bg](img/background_sc19.png)
# The Cinema Ecosystem?
<img src="img/ecosystem.png" width="100%">

---
![bg](img/background_sc19.png)
# Important Terms

- **Cinema database:** a set of data in permanent storage, as described by the Cinema Specification, consisting of **artifacts** and parameters.

- **Artifact (Extract):** a logical collection of data in permanent storage
    - example: a set of images
    - example: a set of graphs
    - example: a simulation grid
    - example: `.vti` file
---
![bg](img/background_sc19.png)
# Online Resources

- This Tutorial
    - https://github.com/cinemascience/cinema_tutorial_2019-11_SC
- Cinema github
    - https://github.com/cinemascience
- Cinema websites
    - http://www.cinemascience.org
    - http://www.cinemaviewer.org
- Cinema Examples
    - http://cinemascience.org/tutorials/2019-11_SC.html
    - http://portal.nersc.gov/project/alpine/2018_ECPReview_Cinema/review.new.html

---
![bg](img/background_sc19.png)
# Cinema Website

<img src="img/cinemawebsite.png" width="50%" align="right">

- Examples (videos)
- Links to code repositories
- Links to expanded documentation

---
![bg](img/background_sc19.png)
# Cinema Website Documentation

<img src="img/cinemawebsite_docs.png" width="50%" align="right">

- Summarized code examples
- Third party partner instructions
	- ParaView
	- VisIt
- Example datasets

---
![bg](img/background_sc19.png)
# Cinema Github Repositories

<img src="img/cinemascience.png" width="50%" align="right">

- `cinemascience` group
- All public released and in-progress code
	- See individual projects for status

---
![bg](img/background_sc19.png)
# Cinema Examples

<img src="img/ecp2018examples.png" width="50%" align="right">

- ECP app examples for 2018 review
- View of ongoing workflow development for ECP app analysis and tasks

---
![bg](img/background_sc19.png)
# How to follow along ...

- In your virtual machine, `cd cinema_tutorial`
- git clone https://github.com/cinemascience/cinema_tutorial_2019-11_SC.git
and follow along in the browser, `https://github.com/cinemascience/cinema_tutorial_2019-11_SC/tutorial.html`


---
![bg](img/background_sc19.png)
# A note about Cinema Viewers and browser permissions

- Safari
    - Safari->Preferences->Advanced->Show Develop menu in menu bar
    - Safari->Develop->Disable Local File Restrictions (on)
    - **NOTE:** Reset file restrictions when you are done
- Firefox
    - In address bar, input **about:config:**
		- Change **privacy.file_unique_origin** to **false**
- Chrome (exit Chrome)
    - use --disable-web-security command line option for this session
    - `open_tutorial` file has an example for Mac


---
![bg](img/background_sc19.png)
# Coder Information: Digging into Cinema Databases
<img src="img/coder.png" width="40%" align="right">

A Cinema database is a set of artifacts, parameters and semantics.

- [Cinema Specification](https://github.com/cinemascience/cinema/blob/master/specs/dietrich/01/cinema_specD_v012.pdf)
    - Describes the format (csv), and a minimal set of restrictions on the data.
    - A set of artifacts, and parameters associated with those files.
    - Note that location of artifacts is not restricted by specification (can be local or remote), but for simplicity, this tutorial covers local examples.

---
![bg](img/background_sc19.png)
# A hand-editable example of a Cinema Database

No matter how complex, all Cinema databases have the same elements.

```
example_01.cdb/
    data.csv (parameters)

example_02.cdb/
    data.csv (parameters)
    01.png   (artifact files)
    02.png
    03.png
    ...
```

Other data can reside in the `<>.cdb` directory, and is not controlled by the spec.

---
![bg](img/background_sc19.png)
# How would you create one from scratch?

- Use Case: you have a set of images defined by some parameters (say, time ...)

```
data/
    x-42.png
    x-43.png
    x-44.png
    x-45.png
    x-46.png
    x-48.png
...
```

---
![bg](img/background_sc19.png)
# Cinema Database

Create a `data.csv` file, according to the specification:

Format is `(parameters)(artifacts)`.

```
time,FILE
42,x-42.png
43,x-43.png
44,x-44.png
45,x-45.png
46,x-46.png
48,x-48.png
49,x-49.png
50,x-50.png
52,x-52.png
53,x-53.png
...
```
---
![bg](img/background_sc19.png)
# That's it ...

```
data/
    data.csv
    x-42.png
    x-43.png
    x-44.png
    x-45.png
    x-46.png
    x-48.png
...
```

---
![bg](img/background_sc19.png)
# Now you can explore this in a viewer

<img src="img/halo.png" width="600" align="right">

Explore this with a Cinema viewer, and scroll through the images using the parameter sliders.

- `Halo Dataset` link in **tutorial home page**
- Works for any number of parameters
- Works for any number of artifacts

---
![bg](img/background_sc19.png)
# A sample database with a few more parameters

<img src="img/volume.png" width="600" align="right">

- `Volume Dataset` entry in **tutorial home page**

---
![bg](img/background_sc19.png)
# But ... Data Is 'Messy'

- Smoothly varying databases are nice, and typically come from simulations
	- Typically have all values expected - entire `data.csv` is populated
- But real world data can be messy, and this is valid per the spec
    - `NaN`, empty values are fine
    - viewers, algs are expected to properly deal with this

```
temp,pressure,vel,time,FILE
3.0,1.0,,1.0,results/1.csv
3.1,2.0,45.6,1.0,results/2.csv
3.3,3.0,45.6,1.0,results/3.csv
4.0,NaN,45.6,1.0,results/4.csv
...
```
---
![bg](img/background_sc19.png)
# A multi-artifact Cinema database

- A database can have multiple artifacts
	- Example: `materials/data/multi_artifact.cdb`
    - The database has the same organization as before:
	- `(set of parameters)(set of artifacts)`

```
theta,phi,vti x-radius,pdb,FILE,FILE_VTI,FILE_PDB
0,-180,10,good,image/-180/0.png,wavelet/10.vti,good.pdb
0,-162,20,N/A,image/-162/0.png,wavelet/20.vti,
0,-144,30,N/A,image/-144/0.png,wavelet/30.vti,
0,-126,40,N/A,image/-126/0.png,,
...
```

---
![bg](img/background_sc19.png)
# Cinema Explorer viewer supports multiple data types

<img src="img/explorer_multiple.png" width="50%" align="right">

- `Cinema Explorer` link in **tutorial home page**
- select "Multiple Artifacts" from the database list at the top, press `load` button

---
![bg](img/background_sc19.png)
# Cinema Explorer viewer supports multiple data types
<img src="img/explorer_multiple.png" width="50%" align="right">

When viewing this data, `Cinema:Explorer` shows thumbnails for each type of data that it can view.

- Clicking on the thumbnail brings up an appropriate viewer for that type of data, if possible.
- **NOTE:** `Cinema:Explorer` indicates which types of files it doesn't have viewers for.

---
![bg](img/background_sc19.png)
# Cinema Explorer viewer supports multiple data types
<img src="img/explorer_multiple_volume.png" width="50%" align="right">

ParaView/VTK `.vti` files can be interactively viewed ...

---
![bg](img/background_sc19.png)
# Cinema Explorer viewer supports multiple data types
<img src="img/explorer_multiple_molecule.png" width="50%" align="right">
ParaView/VTK `.pdb` files can be interactively viewed ...

---
![bg](img/background_sc19.png)
# How else can we create a Cinema database?
<img src="img/ascent.png" width="50%" align="right">

- Directly output Cinema from your code
    - Refer to the specification
- ASCENT
    - **in-situ** output
- ParaView
    - application
    - **in-situ:** ParaView catalyst (instructions on cinema website)
- VisIt
    - application (instructions on cinema website)

<!-- TODO add montage diagram, including ASCENT example (get from Matt)-->

---
![bg](img/background_sc19.png)
# Application export example


---
![bg](img/background_sc19.png)
# View Resulting Database in `cinema:compare`

<img src="img/compare.png" width="50%" align="right">

- `Sphere Database Comparison` link on **tutorial home page**

<br></br>
<br></br>

## ... so how do we use the viewers?


---
![bg](img/background_sc19.png)
# Cinema Viewers
<img src="img/coder.png" width="30%" align="right">


`cinemascience` github organization includes several viewer repositories

- **Cinema:Components**, reusable browser-based components for viewers.
- **Cinema:Compare**, a basic viewer to compare several databases.
- **Cinema:Explorer**, a more full-featured viewer to explore databases.
- **Cinema:Scope**, a cross-platform viewer application under development.

---
![bg](img/background_sc19.png)
# Cinema Viewers
<img src="img/coder.png" width="30%" align="right">

Viewers and components can be used in a variety of ways:

- Small files saved along with Cinema databases
	- Useful when web access is restricted
    - Requires no infrastructure support
        - Ease of support
        - Long shelf life
- Online, through web server
	- Common use case
    - Cinema will be supported natively on ECP Concur

---
![bg](img/background_sc19.png)
# Coder Information: Cinema Components
<img src="img/components.png" width="35%" align="right">


- `cinema_components` is a set of reusable javascript components
	- artifact query viewer
	- parallel coordinates browser
	- graphs
	- database loading components
- github repository includes detailed examples and docs

---
![bg](img/background_sc19.png)
# Cinema Components
- Repository and examples: `https://github.com/cinemascience/cinema_components`
    - distributed online, so include these in your own viewers with:
```
<head>
<script
src='https://cinemascience.github.io/release/CinemaComponents.v2.6.2.min.js'>
</script>`
</head>
```

---
![bg](img/background_sc19.png)
# Viewer `Cinema:Compare`
<img src="img/compare.png" width="60%" align="right">
Browser-based basic viewer for image-based output

- Basic viewer, can be easily edited to view multiple databases
- Sliders control all windows
- `Cinema:Compare` will do its best to show images as the parameters are manipulated (missing images will not cause problems).

---
![bg](img/background_sc19.png)
# Viewer `Cinema:Compare`
To modify this application, edit the `index.html` file to point to a list of databases you'd like to view:

- tutorial file: `materials/databases.json`

```
<!doctype html>
<html>

<head>
    <meta charset="utf-8">
    <link rel='stylesheet' href='cinema/compare/1.0/css/compare.css'>
    <link rel='stylesheet' href='cinema/compare/1.0/css/common.css'>
    <script src='https://d3js.org/d3.v4.min.js'></script>
</head>
...
    // START: Array of databases to view
    var dataSets = [ "data/sphere.cdb", "data/sphere.cdb" ];
    // END : Array of databases to view
...
```

---
![bg](img/background_sc19.png)
# Viewer `Cinema:Explorer`
<img src="img/explorer.png" width="800" align="right">
Browser-based Explorer for general databases

---
![bg](img/background_sc19.png)
# Cinema:Explorer
To use this application, edit the `databases.json` file referenced in the html:

```
[
    {
        "name" : "sphere",
        "directory" : "data/sphere.cdb"
    },
    {
        "name" : "Sphere Multi-Image",
        "directory" : "data/sphere_multi-image.cdb"
    },
    {
        "name" : "Multiple Artifacts",
        "directory" : "data/multiple_artifact.cdb"
    }
]
```


---
![bg](img/background_sc19.png)
# Cinema:Scope
<img src="img/scope.png" width="50%" align="right">

- Cross-platform Qt-based viewer
- Includes reusable classes for loading and interacting with Cinema databases
- Initial release scheduled for March 2019 Cinema release cycle.
- Travis CI, building on Linux, OSX and Windows

<br>

`git@github.com:cinemascience/cinema_scope.git`


---
![bg](img/background_sc19.png)
# Coder Information: Cinema Algorithms
<img src="img/coder.png" width="30%" align="right">

A command line tool with set of algorithms that operate on Cinema databases.

- algorithms can generate new **artifacts**, as well as new **parameters** about the artifacts.

`git@github.com:cinemascience/cinema_lib.git`

---
![bg](img/background_sc19.png)
# Coder Information: Cinema Algorithms
<img src="img/coder.png" width="30%" align="right">

Cinema command line tool support the following general operations:

- Verification of databases
- Conversion/Upgrade of database formats
- Meta data operations
    - create new parameters, such as change detection, edge detection, etc.
- Artifact operations
    - create new data artifacts, and add them to the database

---
![bg](img/background_sc19.png)
# Cinema Command line tool
<img src="img/command.png" width="40%" align="right">

- Requirements
    - python 3.6
    - advanced features require:
        - nympy, scipy, scikit-image, opencv
- Clone repository, and install with `pip`
	- instructions and examples in repository

<br></br>
`git@github.com:cinemascience/cinema_lib.git`


---
![bg](img/background_sc19.png)
# Cinema Command Line Algorithm Example

- General form of a command:
	- `cinema -d (database) --command (column ID to operate on)
- What happens
	- original `data.csv` is copied to `data.(timestamp)`
	- new data is added to `data.csv`
- Algorithms
	- image-space algorithms are domain independent
	- parameter algorithms are domain independent

---
![bg](img/background_sc19.png)
# Cinema Command Line Algorithm Example

---
![bg](img/background_sc19.png)
# Questions?

---
![bg](img/background_sc19.png)
# Acknowledgements

- Slides created with [`Marp`](https://yhatt.github.io/marp)

- Nyx cosmology simulation code:
 A. S. Almgren, J. B. Bell, M.J. Lijewski, Z. Lukic, E. Van Andel, "Nyx: A Massively Parallel AMR Code for Computational Cosmology" Astrophysical Journal, 765, 39, 2013.  https://amrex-astro.github.io/Nyx/ 
