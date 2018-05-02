# Rutgers Gaia DR2 Hack
This repository contains code and information about the Rutgers Astro
grad student Gaia DR2 hack session. The hack is 11 a.m. until 5 p.m.
on Wednesday, May 9, 2018. Currently we are planning on hosting it
in Serin 401W.

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

## Python virtual environments
You will need to *activate* the `gaia-hack` environment before executing 
any code or serving any Jupyter notebooks. This can be accomplished by 
running:

    source activate gaia-hack

## Jupyter notebooks
You can view execute Jupyter notebooks (formerly IPython notebooks) by 
running the command:

    jupyter notebook

You can specify a browser type or port number by using the flags
        
    jupyter notebook --browser=firefox --port=8888

At this point, Jupyter will serve a notebook at `localhost:8888`. You can 
stop the notebook at any time by using the keyboard command `<Ctrl-c>`.

### Accessing notebooks remotely
Suppose that you want to have a remote computer, such as `gradserv`, serve
up a Jupyter notebook. Rather than forward the X windowing, you can have 
the remote computer forward it to a port which is being "listened to" by
your local machine. In general, this is done by running `ssh` into the 
remote machine like such:

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


