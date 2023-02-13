# prepare_icon_case_study
Prepare case studies for running the ICON model following the MeteoSwiss setup. 

## usage
``/path/to/prepare_case_study.sh YYMMDDHH HH``

-> the last argument refers to the leadtime, default = 2h

## file overview
* ``prepare_case_study.sh`` : default script
* ``prepare_17101512.sh``: Cold-air pool case of Fabian Schoeni's thesis. Analysis from COSMO-1 from 2017. Ice, snow, and lake variables are completely missing, also SMI and land fraction are added. FIS field is taken from ECMWF eas-file. Omega is ignored. (ICON will produce its own estimate.)
* ``prepare_19091212.sh``: Valley-wind case of Tobia Lezuo's thesis. Analysis from COSMO-1 from 2019. Unlike in 2017, lake variables are available.



