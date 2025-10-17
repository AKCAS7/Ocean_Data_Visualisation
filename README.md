Ocean Sensor Data Project
Overview

This repository contains a simulated oceanographic sensor dataset collected from multiple floating devices over several years. The dataset is structured into three normalized tables to illustrate real-world relational database design, which can be used for data analysis, visualization, and experimentation in tools such as Power BI, SQL Server, or Python.

The dataset consists of 80 readings from 10 unique float devices, including associated location and timestamp information. The schema is designed to maintain referential integrity and enable realistic queries for depth, salinity, temperature, pressure, and device usage.

Table Structure
1. FloatDevice

Stores information about individual float devices.

Column Name	Data Type	Description
FloatDeviceID	VARCHAR(10)	Primary key, unique ID of the device
DeviceName	VARCHAR(50)	Name of the device
DeviceModel	VARCHAR(50)	Model identifier
2. Reading

Contains sensor readings collected from float devices.

Column Name	Data Type	Description
ReadingID	INT	Primary key, unique reading ID
FloatDeviceID	VARCHAR(10)	Foreign key referencing FloatDevice(FloatDeviceID)
Depth	DECIMAL(7,2)	Depth at which the reading was taken (in meters)
Salinity	DECIMAL(5,2)	Salinity of the water at the measured depth (PSU)
Temperature	DECIMAL(5,2)	Water temperature at the measured depth (°C)
Pressure	DECIMAL(7,2)	Water pressure at the measured depth (dbar)
Timestamp	DATETIME	Date and time when the reading was collected
3. Location

Stores the geographical location of each reading.

Column Name	Data Type	Description
LocationID	VARCHAR(10)	Primary key, unique location ID
ReadingID	INT	Foreign key referencing Reading(ReadingID)
Latitude	DECIMAL(9,4)	Latitude of the reading (in decimal degrees)
Longitude	DECIMAL(9,4)	Longitude of the reading (in decimal degrees)
Relationships

FloatDevice → Reading

One-to-many relationship: a single float device can have multiple readings.

Reading → Location

One-to-one relationship: each reading has an associated geographical location.

Entity Relationship Diagram (simplified):

FloatDevice
+------------------+
| FloatDeviceID PK |
| DeviceName       |
| DeviceModel      |
+------------------+
        |
        | 1-to-many
        v
Reading
+-------------------+
| ReadingID PK      |
| FloatDeviceID FK  |
| Depth             |
| Salinity          |
| Temperature       |
| Pressure          |
| Timestamp         |
+-------------------+
        |
        | 1-to-1
        v
Location
+------------------+
| LocationID PK    |
| ReadingID FK     |
| Latitude         |
| Longitude        |
+------------------+

Sample Data

FloatDevice: 10 devices (FD1001 to FD1010)

Reading: 80 readings, covering multiple years (2019–2026)

Location: 80 location entries corresponding to each reading

Example: ReadingID 21

FloatDeviceID: FD1001

Depth: 18.45 m

Salinity: 34.25 PSU

Temperature: 19.30 °C

Pressure: 1002.50 dbar

Timestamp: 2021-05-20 10:10:00

Latitude: 16.8712

Longitude: 79.4014

Usage

Database Setup

Run the provided CREATE TABLE scripts for FloatDevice, Reading, and Location.

Insert the sample data in sequential order to maintain foreign key integrity.

Data Analysis / Power BI

Import the database into Power BI or another BI tool.

Visualize readings over time, map locations, or analyze depth, temperature, and salinity trends.

SQL Queries

Example: Find all readings from a specific device:

SELECT r.ReadingID, r.Depth, r.Salinity, r.Temperature, r.Pressure, r.Timestamp
FROM Reading r
WHERE r.FloatDeviceID = 'FD1003';


Example: Map readings by location:

SELECT l.Latitude, l.Longitude, r.Depth, r.Temperature
FROM Location l
JOIN Reading r ON l.ReadingID = r.ReadingID;

Notes

This dataset is simulated for educational and experimental purposes.

Timestamps and locations are structured to create realistic patterns for analysis.

All numeric fields are designed to avoid overflow errors (Depth and Pressure use DECIMAL(7,2)).

License

This project is released under the MIT License — feel free to use, modify, and experiment with the dataset for learning or research.
