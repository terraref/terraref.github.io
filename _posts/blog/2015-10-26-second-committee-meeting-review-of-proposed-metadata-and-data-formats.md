---
layout: post
title: "Second Standards Committee Meeting"
categories: blog
tags: [standards, reference-data]
image: 
  feature: 
date: 2015-10-29T13:50:12-0500

---


* Table of Contents
{:toc}

### Details

* Date: 2015-10-28 19:00 GMT
* Time: 2PM/1PM/12PM/11AM Eastern / Central / Mountain / Pacific
* Attendees: David Lee (ARPA-E), David LeBauer (UIUC), Alex Thomasson (TAMU), Barnabas Pocnos (CMU), Christer Jansson (PNNL), Dan Northrup (ARPA-E), Ed Delp (Purdue), Elodie Gazave (Cornell), Justin Manzo (ARPA-E), Larry Biehl (Purdue), Matt Colgan (BRT), Melba Crawford (Purdue), Mike Gore (Cornell), Elodie Gazave (Cornell)
 
### Agenda

1. Identify each participant's expertise and interests with respect to the committee
2. Review specifications for Lemnatec Field system
   * identify data / meta-data [terraref/reference-data#2](https://github.com/terraref/reference-data/issues/2)
3. Discuss proposed semantics and formats  
    * Meteorological variables [terraref/reference-data#3](https://github.com/terraref/reference-data/issues/3)
    * Imaging and hyperspectral data [terraref/reference-data#14](https://github.com/terraref/reference-data/issues/14)
    * Plant traits [terraref/reference-data#18](https://github.com/terraref/reference-data/issues/18)
    
    
## Background

  * [TERRAref Standards Committee documentation](https://dlebauer.gitbooks.io/terraref-documentation/content/data_standards_committee.html); Please free to make or suggest edits / comments.
  * [Github resources for Reference Data Team](https://github.com/terraref/reference-data)
  * [Danforth plantCV site:](http://plantcv.danforthcenter.org/) PlantCV will be used as proof-of concept pipeline 
  * [Sample data available in Box](https://uofi.box.com/terraref-sample-data). Provides examples of raw data generated by Lemnatec Systems at Danforth and AZ along with data products currently provided by other platforms (e.g. NASA, NEON, etc)
* We will be supporting robotics data, but TERRAref is not necessarily generating it (?)

Q. Christer – molecular phenotyping, including transcriptomics/proteomics/metabolomics – should this be added to the ontology, reference data.  Spatiotemporal, qualitative and quantitative.  Very large dataset.

A. This is not in the scope of the reference data that we are providing, but uses are welcome to develop a proposal.  Talk to Mike Gore, Christer and David Lee about developing a proposal for molecular phenotyping.  This data type is quite specialized.  This could be built in later. TERRAref is currently handling genetic and phenotypic data and trying to link these – there is a possibility for molecular data to be linked using these resources. We don’t want to overlap with KBase and iPlant but we _do_ want to provide users the ability to link to these resources (e.g. through API, unique identifiers, vocabulary thesaurus).  

Q. Justin – Can’t sync content from box

A. Look into changing permission

## Committee Participation

* Identify each participant's expertise and interests with respect to the committee (see list of expertise and interests, below)
 * Participants can edit their expertise [here on Google Drive](https://docs.google.com/spreadsheets/d/14Z-Y2MmVy94X561VJdecBSu577VQ4H6G65gh8p_pkD4/edit?usp=sharing)
  * We need to identify one person from each funded project to be the point person and attend annual meetings.
* Anyone can join monthly calls, be on the email list. We encourage all TERRA research teams as well as other experts and the public to provide feedback  
    * Mike Gore and Elodie Gazave from Cornell will lead proposal for genomics data.

### Suggestions for additional external members?

* We have USDA, NASA, Neon
* External person to represent genomics data
* JGI John Vogel (via Christer Jansson), though is part of a TERRA team
* Others? (via Dan Northrup and David Lee)
* External person to represent robotics

### Specifications Lemnatec Field system


1. [Overview of sensors to be placed on the Lemnatec Field system](/articles/2015-10-26-lemnatec-scanalyzer-field-sensors/)


2.	identify additional data / meta-data that will be required  https://github.com/terraref/reference-data/issues/2
  * Showed location of data in box and how the sensor data is organized.  Each sensor has raw and meta data files.
  * What is important to keep in each of the meta data files besides what is already embedded in the database?  This includes information about the sensors.

* Q. Melba unsure if the data in the folders is the actual output of the sensors.  Are these Headwall output with correcting sensors or straight sensors?  We need to know if it’s already been corrected to that output format.
* David LeBauer will talk with Melba about this and determine how to best follow up.
* TERRAref will not be using Lemnatec’s proprietary software because it is not created for all of the sensors that we are using and because we want to be in control of the algorithms
* TERRAref will process sensor data into datacubes

## Discuss proposed semantics and formats

* Meteorological variables https://github.com/terraref/reference-data/issues/3
  * Ed Delp will look at this in more detail
* 	Imaging and hyperspectral data https://github.com/terraref/reference-data/issues/14
  * Feel free to provide feedback on github
  * Matt Colgan to talk to David LeBauer offline about this
  * Bob Strand is leading this as part of preparing technical documentation for Lemnatec Field system
*	Plant traits https://github.com/terraref/reference-data/issues/18
   * ICASA provides many traits, but not all that we will need.  David Lebuaer suggest to create a table of cross-referring from different databases.
   * What resource should molecular phenotype trait standard names be derived from?

## Other business?

* There will be an in person meeting in Pittsburgh at the Kickoff for data standards at the end of the first day (5 pm).
  * David will give an overview of the data management plan as part of the Cat 5 session earlier in the day, so there may be general interest in this topic.
  * Should the meeting be open to everyone or just the leads?  Space for 25-30
  * David Lee and David LeBauer to work with Rachel Shekar to develop an agenda
* TERRAref needs sample analyses tom better create data products and develop pipelines.
* Would like to better understand how the data will be used.  Please provide feedback on specific applications that the different data types will be used, and in what formats will be most useful.  Also discuss the scope of data that will be used.  For example, will people just need to look in depth at a few plots, or want to regularly analyze the whole field.

## Summary of Action Items

* Mike Gore to propose solution for genomics data
* Melba Crawford to discuss hyperspectral data products with David LeBauer
* Everyone review and update list of members / expertise [Google Drive](https://docs.google.com/spreadsheets/d/14Z-Y2MmVy94X561VJdecBSu577VQ4H6G65gh8p_pkD4/edit?usp=sharing)
* Volunteer to lead domain (or nominate others)
* (All) review and comment on proposed formats in github issues
* Suggest external members (esp. genomics, led by M. Gore)
