# Bing COVID-19 Current Data

### Retrieves the current data shown on [Bing's COVID-19 Tracker](https://www.bing.com/covid) and it is made into a JSON file for usage found [here](https://maanuj-vora.github.io/Bing-COVID-19-Current-Data/currentData.json).

---

![Retrieve Data Hourly](https://github.com/Maanuj-Vora/Bing-COVID-19-Current-Data/workflows/Retrieve%20Data%20Hourly/badge.svg)

All data will be updated hourly, if the thing above is green and says 'passing'.

Site Implementation [Here](https://maanuj-vora.github.io/coronavirus-statistics/currentData.html).

Bing retrieves their data from multiple sources including
 - [CDC](https://www.cdc.gov/coronavirus/2019-ncov/index.html)
 - [WHO](https://www.who.int/emergencies/diseases/novel-coronavirus-2019)
 - [ECDC](https://www.ecdc.europa.eu/en/novel-coronavirus-china)

---

### Link for all JSONs

[Current Data](https://maanuj-vora.github.io/Bing-COVID-19-Current-Data/currentData.json)


[All Names and IDs](https://maanuj-vora.github.io/Bing-COVID-19-Current-Data/allNamesIDs.json)


[Major(Country) Names and IDs](https://maanuj-vora.github.io/Bing-COVID-19-Current-Data/countryNamesIDs.json)*

*If you use the Major(Country) Names and IDs, the order of the countrys/areas are in from most impacted to least impacted


This repository also archives the data each day, and since Bing only provides us with daily data, I do not have access to prior data as of 3/22/2020, but you can access anything from 3/22/2020 onwards, all of these files will be located in the [/docs/archived/](docs/archived/) directory. To use the link you would have to do [https://maanuj-vora.github.io/Bing-COVID-19-Current-Data/archived/mm-dd-yyyy.json](https://maanuj-vora.github.io/Bing-COVID-19-Current-Data/archived/3-22-2020.json)*. 

```javascript

let d = new Date();
strDate = (((d.toLocaleDateString()).replace("/", "-")).replace("/", "-"));

fetch(`https://maanuj-vora.github.io/Bing-COVID-19-Current-Data/archived/${strDate}.json`)
        .then(response => response.json())
        .then(data => {
            //Blah Blah
        });
```

*Note that for the month, you do not need to include a 0 if it is a single digit month.

---

Examples of data retrieval can be found in the [examples](examples/) directory

Usage samples and formatting for jsons can be found at the bottom of the README.md

---

If you have any suggestions, feel free to open up an issue, or make a pull request

---

### Projects utilizing this tool

[+ Add yours](https://github.com/Maanuj-Vora/Bing-COVID-19-Current-Data/edit/master/README.md)

---

### Usage Info

Sample Usage of Retrieving Data of Specific Area using either [all ids](docs/allNamesIDs.json) or [major ids](docs/countryNamesIDs.json).
```javascipt
function getAreaData(id) {
    fetch("https://maanuj-vora.github.io/Bing-COVID-19-Current-Data/currentData.json")
        .then(response => response.json())
        .then(data => {

            var displayName;
            var totalConfirmed;
            var totalDeaths;
            var totalRecovered;
            var lastUpdated;
            var lat;
            var long;
            var parentId;

            if (id == data.id) {
                displayName = (data.displayName);
                totalConfirmed = (data.totalConfirmed);
                totalDeaths = (data.totalDeaths);
                totalRecovered = (data.totalRecovered);
                lastUpdated = (data.lastUpdated);
                lat = (data.lat);
                long = (data.long);
                parentId = (data.parentId);
            }

            else {
                loop1:
                for (y = 0; y < data["areas"].length; y++) {

                    if (id == data["areas"][y].id) {
                        displayName = (data["areas"][y].displayName);
                        totalConfirmed = (data["areas"][y].totalConfirmed);
                        totalDeaths = (data["areas"][y].totalDeaths);
                        totalRecovered = (data["areas"][y].totalRecovered);
                        lastUpdated = (data["areas"][y].lastUpdated);
                        lat = (data["areas"][y].lat);
                        long = (data["areas"][y].long);
                        parentId = (data["areas"][y].parentId);
                        break loop1;
                    }

                    if (data["areas"][y]["areas"].length != 0) {
                        loop2:
                        for (z = 0; z < data["areas"][y]["areas"].length; z++) {

                            if (id == data["areas"][y]["areas"][z].id) {
                                displayName = (data["areas"][y]["areas"][z].displayName);
                                totalConfirmed = (data["areas"][y]["areas"][z].totalConfirmed);
                                totalDeaths = (data["areas"][y]["areas"][z].totalDeaths);
                                totalRecovered = (data["areas"][y]["areas"][z].totalRecovered);
                                lastUpdated = (data["areas"][y]["areas"][z].lastUpdated);
                                lat = (data["areas"][y]["areas"][z].lat);
                                long = (data["areas"][y]["areas"][z].long);
                                parentId = (data["areas"][y]["areas"][z].parentId);
                                break loop1;
                            }
                        }
                    }
                }
            }

            console.log(id);
            console.log(displayName);
            console.log(totalConfirmed);
            console.log(totalDeaths);
            console.log(totalRecovered);
            console.log(lastUpdated);
            console.log(lat);
            console.log(long);
            console.log(parentId);
        });
}
```

Usage for getting all ids and accompanying displayNames
```javascript
fetch("https://maanuj-vora.github.io/Bing-COVID-19-Current-Data/allNamesIDs.json")
        .then(response => response.json())
        .then(data => {
            var id = data["id"];
            var displayName = data["displayName"];
            
            console.log(id);
            console.log(displayName);
        });
```

Format for data json
```
{
  "id": "world",
  "displayName": "Global",
  "areas": [
    {
      "id": "italy",
      "displayName": "Italy",
      "areas": [],
      "totalConfirmed": 59138,
      "totalDeaths": 5476,
      "totalRecovered": 7024,
      "lastUpdated": "2020-03-22T22:59:14.807Z",
      "lat": 43.529028,
      "long": 12.162184,
      "parentId": "world"
    },
    {
      "id": "unitedstates",
      "displayName": "United States",
      "areas": [
        {
          "id": "alabama_unitedstates",
          "displayName": "Alabama",
          "areas": [
            {
              "id": "baldwin_alabama_unitedstates",
              "displayName": "Baldwin",
              "areas": [],
              "totalConfirmed": 2,
              "totalDeaths": 0,
              "totalRecovered": 0,
              "lat": 30.688270568847656,
              "long": -87.74720764160156,
              "parentId": "alabama_unitedstates"
            }...
        }
      ],
      "totalConfirmed": 33382,
      "totalDeaths": 417,
      "totalRecovered": 178,
      "lastUpdated": "2020-03-22T22:59:14.807Z",
      "lat": 39.495915,
      "long": -98.989979,
      "parentId": "world"
    }...
    ],
  "totalConfirmed": 335403,
  "totalDeaths": 14611,
  "totalRecovered": 97636,
  "lastUpdated": "2020-03-22T22:59:14.807Z"
}
```

Format for id and displayNames json
```
{
  "id": [
    "world",
    "chinamainland",
    "italy",
    "unitedstates",
    ...
  ],
  "displayName": [
    "Global",
    "China (mainland)",
    "Italy",
    "United States",
    ...
  ]
}
```

---
