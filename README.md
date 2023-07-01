# Remotely Sensed Crop Stress Early Indicator

Can satellite remote sensing detect early stage crop stress at high resolution across whole-farm scale?

Hydrosat produces a proprietary "fused" thermal infrared land surface temperature (LST) imagery product using sharpening and interpolation algorithms to produce near daily sub-30 m resolution imagery from a combination of MODIS, Sentinel and Landsat imaging platforms. This project aims to explore the input data and intermediate outputs of the algorithms used to produce the LST product in order to detect errors potentially introduced by data quality issues or the application of the algorithms while also exploring applications within agricultural contexts.

See the blog post [here](blog.html).

# Collaborators and Acknowledgements

- [Erik Anderson](https://github.com/eriktuck)
- [Tyler Cruickshank](https://github.com/tcruicks)
- [Joe McGlinchy](https://github.com/joemcglinchy)
We thank Joe McGlinchy of Hydrosat for providing project guidance and data access.

[![DOI](https://zenodo.org/badge/627146632.svg)](https://zenodo.org/badge/latestdoi/627146632)

# Environment
To reproduce this workflow, use the provided `environment.yml` file to create a `conda` environment (you should already have Python and `conda` installed on your system).

After cloning this directory to your system, use the following `bash` commands to create and activate the environment:

```bash
conda env create -f environment.yml
conda activate ea-lst
```

# Data

For access to Hydrosat's proprietary products, you must receive credentials using the instructions described at the [Hydrosat Fusion Hub](https://hydrosat.github.io/fusion-hub-docs/intro.html). Add your credentials to the `secrets/` folder in a file called `creds.json` with the format:

```json
{
    "username":"",
    "password":""
}
```
See the [Hydrosat Fusion Hub Documentation](https://hydrosat.github.io/fusion-hub-docs/intro.html) for additional guidance.

Meteorological data are provided by [Ameriflux](https://ameriflux.lbl.gov/) and included in the project's `data/Ameriflux` directory.

# Workflows
Follow the instructions below to reproduce the workflows in the notebook `blog.ipynb` and convert the Jupyter Notebook to an HTML report.

## Run the analysis
To reproduce the analysis in `blog.ipynb`, first follow the instructions to set up the environment and access data, described above. 

This project uses a configuration file to facilitate repeat workflows on new Ameriflux meteorological towers. To repeat the analysis on a new met tower, add the necessary information to the file `config.yml` by copy/pasting an existing configuration section and updating with the necessary parameters. You must include 
  - the longitude, latitude for the meteorological tower center point, 
  - the the longitude, latitude for the ag field center point, 
  - either a bounding box (list of four coordinates) or area of interest (list of four longitude, latitude pairs), and 
  - the parameters for reading the Ameriflux data. 
  
  In the notebook, change the `met_tower` variable to match. Note that Hydrosat does not currently include coverage for the entire CONUS area.

## Convert to HTML report
To convert the file `blog.ipynb` to an HTML report, you must have the library `nbconvert` installed (note that this library is not included in this project's environment; read the [documentation](https://nbconvert.readthedocs.io/en/latest/) for installation instructions). 

Use the following bash command to convert the notebook:

```bash
jupyter nbconvert --to html_embed --no-input notebook-name.ipynb
```
