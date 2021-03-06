---
layout: post
title: "Producing NEON Data Products"
author: christine_laney
modified:
categories: articles
excerpt:
tags: []
image:
  feature: neon_airborne_observation_platform.jpg
  credit: NEON inc
  creditlink: http://www.neoninc.org/science-design/collection-methods/airborne-remote-sensing
date: 2015-10-02T23:10:47-05:00
---


* Table of Contents
{:toc}


## Producing NEON Data Products


_guest post by Christine Laney, Tim Meehan, and Shelley Petroy covering methods used to create NEON Data Products_

## Background

The Data Products produced by NEON represent the primary scientific deliverable of the Observatory to the user communities it was designed to serve. These Data Products represent the end-to-end flow of data from measurement system design to portal download (http://data.neoninc.org), including the organization of management processes, subsystem interfaces, and the design and implementation of supporting computing infrastructure. 

## Data Product Levels

The Data Products published by NEON include raw measurements and scientific data products from calibrated measurement though higher-level products that combine multiple measurements. NEON has adopted a series of data product processing level descriptions that are consistent with national standards.

* **Level 0 Data** are the data received by the NEON cyberinfrastructure, whether they are generated by automated sensors or entered by a human observer. Level 0 data are provided in the original (engineering) measurement units.
* **Level 1 Data Products** are the initial set of scientifically useful data. These data undergo a quality control process and have been calibrated to scientific units.
* **Level 2 Data Products** are characterized as coming from a single measurement stream/site and native resolution/format. For IS Data Products, this generally means temporal interpolation, for OS Data Products, this means statistics derived from data products at individual sites, and for AOP Data Products, this reflects algorithmic conversion to biogeophysical units, per flightline (native resolution/format).
* **Level 3 Data Products** are also from a single measurement stream/site, but are remapped, regridded, or resized. For IS products, this represents spatial interpolation (e.g. profiles at a tower) and for AOP products, this represents mosaicking of flight lines for the full site.
* **Level 4 Data Products** may be from multiple measurement streams, multiple instances (in time and space, so may include multiple sites), or produced from models. Inputs include Level 1, 2, and 3 products and may also include external datasets.

## Data Product Generation Workflow

* **Data Collection:**  Science designs, requirements (science and technical), and protocols are used to define the measurement infrastructure (towers with sensors, established plots, etc.). Tower sensors are linked via network to NEON HQ, and airborne data are collected and manually transported from the field to NEON. Data generated by field protocols may be manually or automatically collected and transferred to NEON HQ. Data from analyzed samples are returned to NEON by a variety of means from contracted laboratories.
  > Documentation: Science Designs, Science Requirements, Sensor Requirements, Protocols, C3 (Command, Control, and Configuration Document)
* **Data Ingest:** Each subsystem requires a specific data ingest schema, which builds on overall standards (formats, vocabulary, metadata, etc.), but is optimized for data type (continuous sensor streams, image data, etc.). The data are organized into science data, metadata, and ancillary information, and stored within the NEON data stores.
  > Documentation: Algorithm Theoretical Basis Documents (ATBDs), Data Ingest Workbooks, C3 documents
*	**Processing:** Algorithms for processing raw data into data products are prototyped and tested; once finalized, the software is implemented for operational data product processing.
  > Documentation: Algorithm Theoretical Basis Documents (ATBDs) 
*	**Packaging:**  Descriptions of how measurement streams are combined into final data products and definitions of the types of information intended to be provided together as a package are developed and coded to produce the data products.
  > Documentation: Algorithm Theoretical Basis Documents (ATBDs), Data Publication Workbooks
*	**Publication via Data Portal:** Data products are stored in the NEON data archive; data products are retrieved from the NEON data stores and made available to users through the NEON data portal for distribution and download. 

## Inter-team Collaboration
Collaboration between teams to generate data products is coordinated by Integrated Product Teams (IPTs). IPTs are composed of staff from functional disciplines within NEON, working together to build successful data products, identify and resolve issues related to their development, and make sound and timely decisions during the development, production, and delivery process. IPTs are used to provide a common, collaborative working environment for all stakeholder groups involved in product delivery. Each team is responsible for the delivery of a subset of NEON data products and related documentation, and is charged with their delivery within schedule and budget.  

## Illustrated example: Single Aspirated Air Temperature, L0 -> L1

![Image of process](/images/SensorToL1DataProduct.png)

1. Systems Engineering (SYS) and Science (SCI) generate a [Command, Control, and Configuration (C-Cubed)](https://uofi.box.com/C3-singleAspAirTemp) document which is used to instruct sensors on how to operate, e.g., when to sample and how to report results.

2. SYS records characteristics of a deployed sensor, such as sensor identification and general location, in a [Location Hierarchy Definition Document (LHDD)](https://uofi.box.com/CPER-LHDD). LHDD locations have textual named-location information, but can also have numeric geolocation information. A general LHDD guide can be viewed [here](https://uofi.box.com/LHDD-Guide).

3. Additional position information, such as sensor height or depth that is not captured in an LHDD, is recorded by SYS in an [As-Built document](https://uofi.box.com/As-Built-CPER). As-Builts are based on annual deployments of specific sensors. They contain sensor specific information about position, position accuracy, and calibration and transformation coefficients. [Sensor Type Configuration Definition Documents (STCDDs)](https://uofi.box.com/STCDD-sensorPRTtemp) have information on data streaming from each sensor type, such as data format and data stream parsing information when several sensors, and thus several measurements, are located at a single named location.  A general STCDD guide can be viewed [here](https://uofi.box.com/STCDD-guide).

4. The Cyberinfrastructure team (CI) uses LHDDs, STCDDs, and As-Builts to create data structures and metadata, such as Named Locations, in the Asset Management Database (Maximo) and the Processed Data Repository (PDR). CI also uses [Ingest Workbooks](https://uofi.box.com/SAAT-L0), generated as a collaborative effort by Science and Data Products, that define each data stream for any given L0 data product with a term, term description, unit, and data type. These terms are controlled by the data products team, and a recent version of this list (subject to change) can be viewed [here](https://uofi.box.com/NEON-Terms-2015-10-06). These data structures and metadata comprise the Level 0 (L0) Definitional Data (Def Data) that allows the PDR to accept streaming sensor data. There is a fair amount of discussion between all involved teams (including Science, Engineering, Cal-Val, CI, and Data Products) throughout this process, via Integrated Product Teams (IPTs) that work together on batches of data products. 

5. Once L0 data is streaming into the PDR, it is possible to create derived products. Derived products are created by pulling and processing batches of L0 data from PDR, and putting the new L1 data into the PDR using the L1 Def Data as a guide.

6. L1 Def Data is created by CI using the [Publication Workbook](https://uofi.box.com/saat-datapub), provided by SCI. The Publication Workbook is a spreadsheet that defines variable names, types, units, and other characteristics of the L1 data.

7. The algorithms for transitioning L0 data to L1 data are included in an [Algorithm Theoretical Basis Document (ATBD)](https://uofi.box.com/ATBD-SingleAspAIrTemp), provided to CI by SCI. The ATBD might also refer to more general algorithms, such as [quality control algorithms](https://uofi.box.com/NEONDOC000783), that are documented in other ATBDs and referred to as Applicable Documents (AD) items in ATBD text and tables.

8. The Publication Workbook is used by SCI to produce two other documents that are used to create a download package for L1 data (from the [NEON Data Portal](http://data.neoninc.org/home)). This package includes a [Readme file](https://uofi.box.com/NEON-DP1-00002-readme), which is a text document with 1) a dynamic component that describes the data selection characteristics, 2) a static component that gives a general description of the data product and how it was collected, and 3) a dynamic component that documents minor changes in the data that are not large enough to warrant a full revision.

9. The download package also includes a [Variables file](https://uofi.box.com/NEON-DP1-00002-variables) that defines variables in the downloaded data for the end user. The variables file is a spreadsheet file, essentially a subset of the Publication Workbook. 

10. The [Download Package](https://uofi.box.com/SAAT-DataPackageExample) includes the L1 data from the PDR (often as multiple .csv files split by horizontal or vertical location), the Variables file, and the Readme file, the [data policy](https://uofi.box.com/NeonDataPolicy), and, if requested other supporting documents like the ATBD(s). 

For an up-to-date list of L1 through L3 products, visit NEON's [Data Product Catalog](http://data.neoninc.org/data-product-catalog).

See also an overview of NEONs Airborne Remote Sensing platform.
