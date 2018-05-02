# Rutgers Gaia DR2 Hack
This repository contains code and information about the Rutgers Astro
grad student Gaia DR2 hack session. The hack is 11 a.m. until 5 p.m.
on Wednesday, May 9, 2018. Currently we are planning on hosting it
in Serin 401W.


## Table of Contents
#### [Getting started](#getting-started)
#### [Gaia data archives](#gaia-dr2-data)

## Getting started
Please download or clone the repository using:

    git clone https://github.com/rutgers-physics-ml/gaia-dr2-hack

If you have your own Github account, you can fork the repository 
first, and then clone it from your own copy.

You will need Anaconda Python 3.6 or later, and we will supply all
necessary packages. Note that you will need an internet connection.
First add the `conda-forge` and `astropy` channels for access to some 
necessary Python packages:

    conda config --add channels conda-forge
    conda config --add channels astropy

Install the rest of the packages by running:

    conda env create -f environment.yml

These packages have now been installed on your system, to a virtual
environment in Anaconda Python named `gaia-hack`.

### Python virtual environments
You will need to *activate* the `gaia-hack` environment before executing 
any code or serving any Jupyter notebooks. This can be accomplished by 
running:

    source activate gaia-hack

### Jupyter notebooks
You can view execute Jupyter notebooks (formerly IPython notebooks) by 
running the command:

    jupyter notebook

You can specify a browser type or port number by using the flags
        
    jupyter notebook --browser=firefox --port=8888

At this point, Jupyter will serve a notebook at `localhost:8888`. You can 
stop the notebook at any time by using the keyboard command `<Ctrl-c>`.

#### Accessing notebooks remotely
Suppose that you want to have a remote computer, such as `gradserv`, serve
up a Jupyter notebook. This can be accomplishing by "listening in" to a 
remote server port on your local machine. If you want to do this, then
first log in to your remote machine:

    ssh username@gradserv.physics.rutgers.edu

and from there, starting a notebook by running:

    username@gradserv> jupyter notebook --no-browser --port=8890

Note that I've prepended `username@gradserv>` to signify that this should be
done on your *remote* computer. You might notice something about "logging in
with a token"" in the output of this command. Save that link for later.

Open up another terminal window on your local machine and run the following 
`ssh` command to access this port:

    ssh -NfL localhost:8889:localhost:8890 username@gradserv.physics.rutgers.edu

This means that whatever is served to port 8890 of the remote computer,
which in this case should be the Jupyter notebook, is now forwarded to your
local port 8889. Feel free to change the port numbers if you wish, although
it is customary to choose numbers greater or equal to 8888. You can now
open a browser on your local machine to go to `localhost:8889` to open the
Jupyter notebook.

Better yet, copy and paste that link from your first terminal window, which
should look something like `http://localhost:8890/?token=<.......>`. Change
the port number to `8889` and open this in your local browser in order to
authenticate yourself and use the Jupyter notebook.


## Gaia DR2 Data

### The Gaia archives
The archive can be found [here](https://gea.esac.esa.int/archive/). The "basic" 
section of the search is fairly self-explanatory. There are lots of display 
columns you can choose from (i.e., information you care about), and if you want 
to narrow down your search you can add conditions.

### Querying with ADQL
If you want more control (or, for example, to increase the maximum number of 
results from what the basic version allows), you need to use ADQL, the 
astronomical data query language. Below is an example usage:

```SQL
SELECT TOP 500000 source_id,ra,ra_error,dec,dec_error,parallax,parallax_error,phot_g_mean_mag,bp_rp,radial_velocity,radial_velocity_error,phot_variable_flag,teff_val,a_g_val FROM gaiadr2.gaia_source  WHERE (ra>=23.5 AND ra<=26.5 AND dec>=85.5 AND dec<=87.5)
```

Let's break down what this is doing:

```SQL
SELECT TOP 500000
```

This is telling it to limit the results of the query to 500000 sources.

```SQL
source_id,ra,ra_error,dec,dec_error,parallax,parallax_error,phot_g_mean_mag,bp_rp,radial_velocity,radial_velocity_error,phot_variable_flag,teff_val,a_g_val
```

This is a list of the desired columns of information, including the source ID, 
the ra and dec, parallax, etc.

```SQL
FROM gaiadr2.gaia_source
```

This is the data archive within which you are searching. For Gaia DR2, this 
is what you want.

```SQL
WHERE (ra>=23.5 AND ra<=26.5 AND dec>=85.5 AND dec<=87.5)
```

These are the conditions you want. I've applied simple right ascension and 
declination limits. There are lots of other conditions, each one corresponding 
to possible display columns. For example, I could say `WHERE (parallax>=.5)`,
which would limit me to sources with parallax greater than 0.5 arcseconds, or 
equivalently at distances of less than 2 pc. For more examples, see 
the [archive help page](http://gea.esac.esa.int/archive-help/index.html)


