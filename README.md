## TwilightMonitorDatabase

The `TwilightMonitorDatabase` class is designed to manage and organize data collected by a twilight monitor. This class allows you to create a structured database for each day, storing information such as exposure times, mount positions, and electrometer data.

### Features
- **Initialization**: Automatically sets up the required directory structure and loads or creates a database file for the specified date.
- **Adding Exposures**: Easily add new exposures with relevant data such as timestamp, altitude, azimuth, and electrometer readings.
- **Updating Exposures**: Update existing exposures by specifying the `seq_id` and the fields to modify.
- **Data Persistence**: Automatically saves the database to a CSV file, ensuring that your data is preserved between sessions.

### Example Usage

#### Initialization

To initialize the database for a specific date:

```python
from datetime import datetime
from twilight_monitor import TwilightMonitorDatabase

# Initialize the database for July 21, 2024
db = TwilightMonitorDatabase(21, 7, 2024)
"""
```
#### Add a new exposure
To add a exposure you can simply enter the following information.
```python
# Add a new exposure
db.add_exposure(
    timestamp=datetime.utcnow(),
    alt=45.0,
    az=90.0,
    exp_time_cmd=30,
    filter_type='SDSSr',
    current_mean=0.5,
    current_std=0.01
)
```
#### Updating an Exposure
To update an existing exposure, use the update_exposure method by specifying the seq_id and the fields you want to update:
```python
# Update an existing exposure
db.update_exposure(seq_id=1, current_mean=0.55, current_std=0.02)
```

## Data Structure
The database will be rooted in a twmdb-python folder with the following file tree.

```
.
├── README.txt
├── twmdb.py
└── DATA
    ├── YYYYMM
    │   ├── YYYYMMDD.csv
    │   ├── notes.txt
    │   └── tmp
    │       └── seq_id_XXXXX.csv
```

## Database CSV file information
Every time you close or save the database, a CSV file with panda data frame format is saved. The description of the the CSV file columns is:
* `tmid`: Twilight monitor unique IDs defined by the date and time of exposure start, i.e., YYYYMMDDHHMMSS
* `date`: Timestamp with date and time in UTC.
* `seq_id`: sequence id of the exposure number of the day.
* `exp_time_cmd`: Exposure time commanded (exp_time_commanded).
* `exp_time`: Actual exposure time.
* `filter`: the filter used in the exposure (options include: SDSS{u/g/r/i/z/y} and Empty)
* `alt`: commanded elevation in deg with the format of 0.5f
* `az`: commanded azimuth in def with the format of 0.5f
* `current_mean`: mean current measured by the electrometer during the exposure period. The units are in nano ampere.
* `current_std`: current standard deviation of the electrometer output during the exposure period. The units are in nano ampere.
* `alt_std`: standard deviation of the altitude values in degrees during the exposure period.
* `az_std`:  standard deviation of the azimuth values in degrees during the exposure period.
* `electrometer_filename`: filename of the electrometer output.
* `flag`: TBD

