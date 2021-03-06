---
layout: post
title: "Spectral Imaging: Data Volume, Formats, and Compression"
modified:
categories: articles
excerpt:
tags: field scanner, data
image:
  feature:
date: 2015-10-13T22:22:27-05:00
---

* Table of Contents
{:toc}

## Hyperspectral Data formats
 
HDF5 is a common format for sensor data, and netCDF-4 is one interface to HDF5; in other words, a netCDF-4 file can be treated as an HDF5 file.  These files can store high dimensional data (e.g. time, xyz space, wavelength) and can be written and read in parallel. NetCDF also has tools and specifications that support data use and interoperability in addition to efficient storage and computation.

We will work in part with the NetCDF Operator utilities (NCO, nco.sourceforge.net).
NCO provides functions that compress and reformat data in facilitate on-disk / within file computing for large and heirarchical data sets. This will reduce data volume and increase the speed at which data can be written using specialized hardware and parallel writing. The specialist can also assist researchers to compute on the large data sets when they come on line.

Here is a working proposal for a standardized (CF compliant) file format (NetCDF-4 or HDF5).

Following CF naming conventions [1], these would be in a netcdf-4 compatible / well behaved hdf format. Also see [2] for example formats by NOAA

## Radiance data

### Variables

| variable name | units | dim 1 | dim 2 | dim 3 | dim 4 | dim 5 |
|----|----|----|----|----|----|----|----|
| surface_bidirectional_reflectance   |  0-1 |  lat   | lon   | time   |  radiation_wavelength |  
| upwelling_spectral_radiance_in_air | W m-2 m-1 sr-1 |  lat   | lon   | time   |  radiation_wavelength | zenith_angle |

note: upwelling_spectral_radiance_in_air may only be an intermediate product (and perhaps isn't exported from some sensors?) so the focus is really on the reflectance as a Level 2 product.


### Dimensions 

| dimension | units |  notes |
|----|----|---| 
| latitude | degrees north |   (or alt. projection_y_coordinate) | 
| longitude | degrees east |  (or alt. porjection_x_coordinate below)|
| _projection_x_coordinate_ | m | can be mapped to lat/lon with grid_mapping attribute |
| _projection_y_coordinate_ | m |   can be mapped to lat/lon with grid_mapping attribute | 
| time | hours since 2016-01-01|  
| radiation_wavelength | m  |
| zenith_angle | degrees |
|  _optional_  |    |
|  sensor_zenith_angle | degrees |
|  platform_zenith_angle | degrees  |  

[1] http://cfconventions.org/Data/cf-standard-names/29/build/cf-standard-name-table.html
[2] http://www.nodc.noaa.gov/data/formats/netcdf/v1.1/


## On the Upcoming Data Deluge

Originally the TERRAref team planned to handle a data stream of 1 TB per day for six months per year.
Over the four year project this would generate 730 TB of primary data, and we planned to host this and derived data products (1PB total) on a platform that would allow researchers access the entire dataset from a high performance computer.

Recently, Lemnatec Engineers increased the estimated rate of data generated by the platform to 3-4 TB/day. In addition, the team has extended the duration of observation from 6 to 12 months per year. This amounts to between six to eight more data than originally expected. 

Our original plan was to store these data for active computation, so that researchers would have access to the entire dataset. However, our original solution would expensive - at this scale, it is more efficient to employ specialists to work on efficient data storage.
We will to evaluate methods of reducing data volume through compression and packing, less expensive storage media and archival storage, scheduled computation, and apply for storage space on externally funded research supercomputing platforms.
The revised plan would apply primarily to the imaging spectrometer and laser scanning data sets. Other data sets including RGB, multi-spectral, and thermal images as well as trait vectors that are used for genomic analysis would be available for the duration of the study as originally proposed.
 
For the hyper spectral and 3D imaging datasets, we would optimize storage and access. Researchers could access a subset of these data (primarily the most recent few months). If there is demonstrated need, we would coordinate bringing data on line once per year, and assist researchers in applying calibrated algorithms and/or transferring data to other locations.

### On Data Compression in Memory

It will be prudent to compress files before transfer, indeed, before writing to disk if possible.

Currently we estimate that the hyperspectral sensor could take 48 hours to scan the field at full (mm scale) resolution. The speed of writing limits the rate of data collection.
If we can reduce the amount of data that is written, and also parallelize streams to a file.

It will be prudent to have the necessary hardware co-located to the sensors. Of the shel computers with 32 or 64 GB of ram and 1 TB of solid state drive would be a good place to start. We can also test hardware at NCSA and on the XSEDE network of supercomputers; "Bridges" at the Pittsburgh supercomputing sensor will have 12TB of RAM - enough to store an entire field scan in memory (!)
We will also evaluate compression algorithms embedded in hardware.

If we want to keep all of the data, we need to revisit the data management as originally proposed. Scaling up the proposed online storage from 1 to 10PB would require millions of additional dollars. And some scenarios (if running 12 mo/y) put the top end upwards of 40PB. We will balance the data we plan to keep, how the data are stored, and when it can be accessed. Offline tape storage cost the least to store but requires intensive management to maintain and load for computation. However, if we move data around on a coordinated schedule (e.g. bringing data online once per year for computing) this option would allow us to at least capture the data. 

Regarding lossy compression, we can be sensible about what data we need to keep. For example, if the sensor measures reflectance with an accuracy of 1%, we should be able to truncate precision at 0.1%. This is technically 'lossy' although still "lossless" with respect to scientific meaning relevant to plant phenotyping. There are also opportunities to do 'bin' data over pixels and in space. This effectively reduces resolution, but can be done using a stratefied approach to keep high resolution in interesting parts of space and wavelengths.

With lossy compression, we are not referring to JPG, which is tuned to retain information required for humans to interpret and is therefore not satisfactory for analysis (as demonstraetd by Noah Fahlgren et al). Unlike RGB sensors (which are much more orthogonal and uncorrelated by design), a hyperspectral data cube and time series make these data more amenable to compression by taking advantage of filtering and correlation.

## Some example code used to compress NEON sensor data.

Requires that netcdf, hdf5, and NCO are installed.

{% highlight sh %}

# Download sample Hyperspectral data from NEON
# http://neondataskills.org/HDF5/Plot-Hyperspectral-Pixel-Spectral-Profile-In-R/

curl -O http://neonhighered.org/Data/HDF5/SJER_140123_chip.h5

## Commands tested:

## uncompress
time ncks -O SJER_140123_chip.h5 uncompressed.h5
## two types of compression
time ncks -O -L 1 uncompressed.h5 compressedL1.h5
time ncks -O --ppc default=3 uncompressed.h5 compressed_ppc3.h5

\ls -ltr *.h5

time ncdump -v Reflectance uncompressed.h5 > foo
time ncdump -v Reflectance compressedL1.h5 > foo
time ncdump -v Reflectance compressed_ppc3.h5 > foo

{% endhighlight %}

### Further reading and Feedback 

* Notes on existing standards and formats: https://github.com/terraref/documentation/blob/master/existing_data_standards.md#sensor-data
* Example data products from other programs (NASA, NEON, etc): https://uofi.app.box.com/files/0/f/4299753901
* proposed format for hyperspectral data: https://github.com/terraref/reference-data/issues/14
* proposed meta-data content for Lemnatec system: https://github.com/terraref/reference-data/issues/2
