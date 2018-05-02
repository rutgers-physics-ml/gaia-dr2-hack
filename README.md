# If you want to query the archive:

## Basics

The archive can be found [here](https://gea.esac.esa.int/archive/). The "basic" section of the search is fairly self-explanatory. There are lots of display columns you can choose from (i.e., information you care about), and if you want to narrow down your search you can add conditions.

## Querying with ADQL

If you want more control (or, for example. to increase the maximum number of results from what the basic version allows), you need to use ADQL, the astronomical data query language. Below is an example usage.

`SELECT TOP 500000 source_id,ra,ra_error,dec,dec_error,parallax,parallax_error,phot_g_mean_mag,bp_rp,radial_velocity,radial_velocity_error,phot_variable_flag,teff_val,a_g_val FROM gaiadr2.gaia_source  WHERE (ra>=23.5 AND ra<=26.5 AND dec>=85.5 AND dec<=87.5)`

Let's break down what this is doing:

`SELECT TOP 500000`

This is telling it to limit the results of the query to 500000 sources.

`source_id,ra,ra_error,dec,dec_error,parallax,parallax_error,phot_g_mean_mag,bp_rp,radial_velocity,radial_velocity_error,phot_variable_flag,teff_val,a_g_val`

This is a list of the desired columns of information, including the source ID, the ra and dec, parallax, etc.

`FROM gaiadr2.gaia_source`

This is the data archive within which you are searching. For Gaia DR2, this is what you want.

`WHERE (ra>=23.5 AND ra<=26.5 AND dec>=85.5 AND dec<=87.5)`

These are the conditions you want. I've applied simple right ascension and declination limits. There are lots of other conditions, each one corresponding to possible display columns. For example, I could say
`WHERE (parallax>=.5)`,
which would limit me to sources with parallax greater than 0.5 arcseconds, or equivalently at distances of less than 2 pc. For more examples, see [here](http://gea.esac.esa.int/archive-help/index.html)


