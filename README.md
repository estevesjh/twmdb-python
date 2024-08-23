# Twilight Monitor Database
The Twilight Monitor database is a Python class that reads a CSV file containing all the exposure information for a given day. The following sections will describe the database data structure and its information. 

## Data Structure
The database will be rooted in a twmdb-python folder with the following file tree.
.
├── README.txt
├── twmdb.py
└── DATA
    ├── YYYYMM
    │   ├── YYYYMMDD.csv
    │   ├── notes.txt
    │   └── tmp
    │       └── seq_id_XXXXX.csv


## Database CSV file information
The twilight monitor database should have the following fields
* tmid: Twilight monitor unique IDs defined by the date and time of exposure start, i.e., YYYYMMDDHHMMSS
* date: Timestamp with date and time in UTC.
* seq_id: sequence id of the exposure number of the day.
* exp_time_cmd: Exposure time commanded (exp_time_commanded).
* exp_time: Actual exposure time.
* filter: the filter used in the exposure (options include: SDSS{u/g/r/i/z/y} and Empty)
* Alt: commanded elevation in deg with the format of 0.5f
* Az: commanded azimuth in def with the format of 0.5f
* current_mean: mean current measured by the electrometer during the exposure period. The units are in nano ampere.
* current_std: current standard deviation of the electrometer output during the exposure period. The units are in nano ampere.
* alt_std: standard deviation of the altitude values in degrees during the exposure period.
* az_std:  standard deviation of the azimuth values in degrees during the exposure period.
* electrometer_filename: filename of the electrometer output.
* flag: TBD

## The script
The Python class should require minimal initialization, with only the date, day, month, and year. After that, the user can add exposures to the database. 

Initialization
The user will provide the year, month, and day in the initialization process. The Python class will then check if a folder for that month and a CSV file for that day already exist; if not, it will create these files. Each step of this class will be saved to a log file using the logger class. Once the class is initialized with a self.database (data frame) file, it will be ready to add new exposures.

Add new exposures
The minimal input for a new exposure in the database is a timestamp (date and time UTC), alt and az. The filter will be predefined as “Empty”. All the other fields will have nan values and they will be updated once the exposure is completed. 
