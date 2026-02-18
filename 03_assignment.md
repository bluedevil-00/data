```python
# PART 1: WORKING WITH JSON DATA
```


```python
import requests
```


```python
import json
```


```python
# Here's a sample JSON structure similar to what APIs return
sample_json = '''
{
  "station": "USC00305800",
  "name": "New York Central Park",
  "location": {
    "latitude": 40.7789,
    "longitude": -73.9692
  },
  "observations": [
    {"date": "2023-01-01", "temperature": 32, "precipitation": 0.0},
    {"date": "2023-01-02", "temperature": 28, "precipitation": 0.5},
    {"date": "2023-01-03", "temperature": 35, "precipitation": 0.0},
    {"date": "2023-01-04", "temperature": 38, "precipitation": 0.2},
    {"date": "2023-01-05", "temperature": 41, "precipitation": 0.0}
  ]
}
'''

# Parse the JSON
data = json.loads(sample_json)

# Access nested data
print("Station:", data['station'])
print("Location:", data['location'])
print("First observation:", data['observations'][0])
```

    Station: USC00305800
    Location: {'latitude': 40.7789, 'longitude': -73.9692}
    First observation: {'date': '2023-01-01', 'temperature': 32, 'precipitation': 0.0}



```python
# 1. Extract and print all dates and temperatures (8 points)
print("Date, Temperature")
for obs in data['observations']:
    # YOUR CODE HERE: print date and temperature for each observation
    print(obs['date'], obs['temperature'])
```

    Date, Temperature
    2023-01-01 32
    2023-01-02 28
    2023-01-03 35
    2023-01-04 38
    2023-01-05 41



```python
# 2. Calculate average temperature (8 points)
total_temp = 0
count = 0
# YOUR CODE HERE: calculate average
for obs in data ['observations']:
    total_temp += obs['temperature']
    count += 1
avg_temp = total_temp/count
print(f"Average temperature: {avg_temp}°F")
```

    Average temperature: 34.8°F



```python
# 3. Find days with precipitation (9 points)
print("\nDays with precipitation:")
# YOUR CODE HERE
precip_days = 0

for obs in data ['observations']:
    if obs['precipitation'] > 0:
        precip_days = precip_days + 1
print(precip_days)
```

    
    Days with precipitation:
    2



```python
# Use a real weather API (you may need to sign up for a free API key)
# Example APIs: OpenWeatherMap, NOAA, Weather.gov
# YOUR CODE HERE

# url = "https://api.weather.gov/zones/forecast/{zoneId}/stations

{
  "@context": [
    "string"
  ],
  "type": "FeatureCollection",
  "features": [
    {
      "@context": [
        "string"
      ],
      "id": "string",
      "type": "Feature",
      "geometry": {
        "type": "Point",
        "coordinates": [
          0,
          0
        ],
        "bbox": [
          0,
          0,
          0,
          0
        ]
      },
      "properties": {
        "@context": [
          "string"
        ],
        "geometry": "string",
        "@id": "string",
        "@type": "wx:ObservationStation",
        "elevation": {
          "value": 0,
          "maxValue": 0,
          "minValue": 0,
          "unitCode": "nwsUnit:RX%of\\/V,1AU/;G`?5.fE1=.L23715t CHK)cKvtio+k9%t_49YWw+~4pE7",
          "qualityControl": "Z"
        },
        "stationIdentifier": "string",
        "name": "string",
        "timeZone": "string",
        "provider": "string",
        "subProvider": "string",
        "forecast": "string",
        "county": "string",
        "fireWeatherZone": "string",
        "distance": {
          "value": 0,
          "maxValue": 0,
          "minValue": 0,
          "unitCode": "_bFzJ~$clW7",
          "qualityControl": "Z"
        },
        "bearing": {
          "value": 0,
          "maxValue": 0,
          "minValue": 0,
          "unitCode": "nwsUnit:lyD3zs,z8B}6\\O>gw|%51yRL1v/CnveUTA| )\\!fHu`u0/,6kqVHf}4Q2HK,B",
          "qualityControl": "Z"
        }
      }
    }
  ],
  "observationStations": [
    "string"
  ],
  "pagination": {
    "next": "string"
  }
}
# run this code, output below:
```




    {'@context': ['string'],
     'type': 'FeatureCollection',
     'features': [{'@context': ['string'],
       'id': 'string',
       'type': 'Feature',
       'geometry': {'type': 'Point', 'coordinates': [0, 0], 'bbox': [0, 0, 0, 0]},
       'properties': {'@context': ['string'],
        'geometry': 'string',
        '@id': 'string',
        '@type': 'wx:ObservationStation',
        'elevation': {'value': 0,
         'maxValue': 0,
         'minValue': 0,
         'unitCode': 'nwsUnit:RX%of\\/V,1AU/;G`?5.fE1=.L23715t CHK)cKvtio+k9%t_49YWw+~4pE7',
         'qualityControl': 'Z'},
        'stationIdentifier': 'string',
        'name': 'string',
        'timeZone': 'string',
        'provider': 'string',
        'subProvider': 'string',
        'forecast': 'string',
        'county': 'string',
        'fireWeatherZone': 'string',
        'distance': {'value': 0,
         'maxValue': 0,
         'minValue': 0,
         'unitCode': '_bFzJ~$clW7',
         'qualityControl': 'Z'},
        'bearing': {'value': 0,
         'maxValue': 0,
         'minValue': 0,
         'unitCode': 'nwsUnit:lyD3zs,z8B}6\\O>gw|%51yRL1v/CnveUTA| )\\!fHu`u0/,6kqVHf}4Q2HK,B',
         'qualityControl': 'Z'}}}],
     'observationStations': ['string'],
     'pagination': {'next': 'string'}}




```python
# PART 2: DOWNLOADING FILES WITH PYTHON
```


```python
import pooch
import os

# Set up Pooch to download a file
# This example downloads a small air quality dataset
file_path = pooch.retrieve(
    url="https://github.com/pandas-dev/pandas/raw/main/doc/data/air_quality_no2.csv",
    known_hash=None
)

print("File downloaded to:", file_path)
print("File exists:", os.path.exists(file_path))
```

    File downloaded to: /home/cjt2162/.cache/pooch/458dad453f6a48e510cd544bef1854e3-air_quality_no2.csv
    File exists: True



```python
# 1a. Verify the file was downloaded (5 points)
print("File downloaded to:", file_path)
print("File exists:", os.path.exists(file_path))

# Check the file size
file_size = os.path.getsize(file_path)
print(f"File size: {file_size} bytes")
```

    File downloaded to: /home/cjt2162/.cache/pooch/458dad453f6a48e510cd544bef1854e3-air_quality_no2.csv
    File exists: True
    File size: 31984 bytes



```python
# 1b. YOUR CODE HERE: open the file and count how many lines it has
line_count = 0

with open(file_path, "r") as f:
    for line in f:
        line_count += 1

print(f"Number of lines: {line_count}")
```

    Number of lines: 1036



```python
# 2a. Download another file (10 points)
# Find a climate dataset online using the sources we talked about in lecture
# Download it using Pooch

# YOUR CODE HERE:
# my_url = "..."
# my_file = pooch.retrieve(url=my_url, known_hash=None)  # hash optional for first try

my_url = "https://data.nasa.gov/docs/legacy/meteorite_landings/Meteorite_Landings.csv" 
my_file = pooch.retrieve(url=my_url, known_hash=None)

print("File downloaded to:", my_file)
print("File exists:", os.path.exists(my_file))
```

    File downloaded to: /home/cjt2162/.cache/pooch/a19fd2df36fd8edbdc8806f06d01424b-Meteorite_Landings.csv
    File exists: True



```python
#2b. Print info about your downloaded file
file_size = os.path.getsize(my_file)
print(f"File size: {file_size} bytes")

line_count = 0
with open(my_file, "r") as f:
    for line in f:
        line_count += 1
print(f"Number of lines: {line_count}")
```

    File size: 3952161 bytes
    Number of lines: 45717



```python
# 3. Create a data inventory (5 points)
# List all the files you've downloaded in this assignment
print("\nData Inventory:")
print("1. meteorites.csv - NASA meteorite landings")
print("2. air_quality_no2.csv - Air quality NO2 measurements")
# YOUR CODE HERE: add your file from task 2
print("3. Meteorite_Landings.csv - NASA meteorite landings") 
```

    
    Data Inventory:
    1. meteorites.csv - NASA meteorite landings
    2. air_quality_no2.csv - Air quality NO2 measurements
    3. Meteorite_Landings.csv - NASA meteorite landings



```python
# PART 3: UNDERSTANDING NetCDF METADATA
```


```python
import requests

# OPeNDAP provides metadata in different formats
# We'll get basic info about a climate dataset

base_url = "http://iridl.ldeo.columbia.edu/expert/SOURCES/.NOAA/.NCEP/.CPC/.UNIFIED_PRCP/.GAUGE_BASED/.GLOBAL/.v1p0/.Monthly/.RETRO/.rain/dods"

# Get DDS (Dataset Descriptor Structure) - describes the structure
dds_url = base_url + ".dds"
response = requests.get(dds_url)

print("Dataset Structure:")
print(response.text[:500])  # Print first 500 characters
```

    Dataset Structure:
    Dataset {
        Float32 T[T = 324];
        Float32 Y[Y = 360];
        Float32 X[X = 720];
        Grid {
         ARRAY:
            Float32 rain[T = 324][Y = 360][X = 720];
         MAPS:
            Float32 T[T = 324];
            Float32 Y[Y = 360];
            Float32 X[X = 720];
        } rain;
    } rain;
    



```python
# 1. Identify dimensions and variables (5 points)
# Look at the DDS output above and answer:
# - What are the dimension names?
# - What is the main variable name?
# - Write your answers in a markdown cell
```

Identify dimensions and variables (5 points)  
Look at the DDS output above and answer:  
* What are the dimension names? **T (time), Y (longitude), X (latitude)**  
* What is the main variable name? **rain**  


```python
# 2. Get data attributes (5 points)
# DAS (Dataset Attribute Structure) contains metadata
das_url = base_url + ".das"
# YOUR CODE HERE: make a request to das_url and print first 1000 characters
response = requests.get(das_url)

print("Dataset Attribute Structure:")
print(response.text[:1000])  # Print first 1000 characters
```

    Dataset Attribute Structure:
    Attributes {
        X {
            String standard_name "longitude";
            Float32 pointwidth 0.5;
            Int32 gridtype 1;
            String units "degree_east";
        }
        T {
            Float32 pointwidth 1.0;
            String calendar "360";
            Int32 gridtype 0;
            String units "months since 1960-01-01";
        }
        Y {
            String standard_name "latitude";
            Float32 pointwidth 0.5;
            Int32 gridtype 0;
            String units "degree_north";
        }
        rain {
            Int32 pointwidth 0;
            String standard_name "lwe_precipitation_rate";
            Float32 file_missing_value -999.0;
            String history "Boxes with less than 0.0% dropped";
            Float32 missing_value NaN;
            String units "mm/day";
            String long_name "Monthly Precipitation";
        }
    NC_GLOBAL {
        String Conventions "IRIDL";
    }
    }
    



```python
# 3. Document what you learned (5 points)
# In a markdown cell, write:
# - What does this dataset contain?
# - What time period does it cover?
# - What geographic region does it cover?
# - What are the units of the main variable?
# Find this info in the DAS output
```

Document what you learned (5 points)
* What does this dataset contain? **monthly precipitation data (variable 'rain', name lwe_precipitation_rate)**
* What time period does it cover? **monthly readings starting in 1/1/1960 and progressing monthly (months since 1960-01-01)**
* What geographic region does it cover? **the dataset coverage is global (worldwide latitude and longitude grid)**
* What are the units of the main variable? **main variable = rain, units = mm/day (millimeters/day)**
