I am tired of re-learning how to download ERA5 data, so here is the download script I use every time (all you need to do is change the variable and times).

### If you don't already have it (this can be done directly in a jupyter notebook):
```bash
pip install cdapi
```
### Then you need to make sure the api client knows who you are (find all pertinent information at: https://cds.climate.copernicus.eu/how-to-api)
```bash
import cdsapi

# Replace with your real API key
api_key = "API KEY" # make sure you log in to get your api key

c = cdsapi.Client(
    url="https://cds.climate.copernicus.eu/api/",
    key=api_key
)
```
### Then you can download your data to your desired output directory (see the jupyter notebook) but essentially:
```bash
import cdsapi
import os

dataset = "reanalysis-era5-single-levels"
request = {
    "product_type": ["reanalysis"],
    "variable": ["mean_sea_level_pressure"],
    "year": [
        "2017"
    ],
    "month": [
        "01", "02", "03",
        "04", "05", "06",
        "07", "08", "09",
        "10", "11", "12"
    ],
    "day": [
        "01", "02", "03",
        "04", "05", "06",
        "07", "08", "09",
        "10", "11", "12",
        "13", "14", "15",
        "16", "17", "18",
        "19", "20", "21",
        "22", "23", "24",
        "25", "26", "27",
        "28", "29", "30",
        "31"
    ],
    "time": [
        "00:00", "06:00", "12:00",
        "18:00"
    ],
    "data_format": "netcdf",
    "download_format": "unarchived"
}

target = "/OUTPUT_DIR/era5_msl_2017_6hourly.nc"
os.makedirs(os.path.dirname(target), exist_ok=True)
# client = cdsapi.Client()

c.retrieve(dataset, request, target)

```

### and that is kind of all there is to it, and this is probably way more helpful for me than anyone else out there.
