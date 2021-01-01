# handy - utilities for handheld radio

_WARNING! This code is kludged together, it is not idiomatic in any way and was born purely out of immediate necessity._

## install

- ensure internect connectivity
- ensure you have "a recent" nodejs/npm installed
- `git clone git@github.com:m7xer/handy.git`
- `cd handy`
- `npm install`


## scripts

### generateChirpCSV

Generate CSV for CHIRP programming, with the 60 most local UK repeaters and a bunch of satellites with Doppler adjusted downlinks.

Usage:
Pass in your UK [Maidenhead locator](https://www.levinecentral.com/ham/grid_square.php) to obtain the nearest 2M and 70CM analogue voice repeaters for you. Satellite data will be augmented before the final CSV is generated. Modify the script for more features as YMMV!

`
./scripts/generateChirpCSV IO92BL
`

Example Output:
```
$ ./scripts/generateChirpCSV IO92BL
#####
UK Maidenhead locator required for best results! for example:
./scripts/generateChirpCSV IO92BL
home location calculated from IO92BL as {"lat":52.458333333333336,"lon":-1.9166666666666667}
allRepeaters 623
SAVED to scratchpad/allRepeaters_1609499026963.json:
[{"repeater":"GB3AA","band":"2M","channel":"RV53","TX":"145.6625","RX":"145.0625","mode":"AV","QTHR":"IO81RO","where":"BRISTOL","region":"SW","code":"94.8","keeper":"G4CJZ","lat":"51.59","lon":"-2.54","":""},{"repeater":"GB3AB","band":"70CM","channel":"RB0
...SNIPPED...
r":"M0JBR","lat":"50.87","lon":"0.56","":""},{"repeater":"GB7ZP","band":"70CM","channel":"DVU39","TX":"439.4875","RX":"430.4875","mode":"DSTAR","QTHR":"JO01GQ","where":"CHELMSFORD","region":"SE","code":"","keeper":"G6JYB","lat":"51.71","lon":"0.50","":""}]

suitableRepeaters 60
SAVED to scratchpad/suitableRepeaters_1609499026968.json:
[{"repeater":"GB3CB","band":"70CM","channel":"RB14","TX":"433.3500","RX":"434.9500","mode":"AV","QTHR":"IO92BL","where":"BIRMINGHAM","region":"MIDL","code":"67","keeper":"G8NDT","lat":"52.46","lon":"-1.89","":"","distance":1816.2539887041903},{"repeater":"
...SNIPPED...
1.61854566132},{"repeater":"GB3AB","band":"70CM","channel":"RB07","TX":"433.1750","RX":"434.7750","mode":"AV","QTHR":"IO93FK","where":"SHEFFIELD","region":"NOR","code":"82.5","keeper":"M0GAV","lat":"53.42","lon":"-1.54","":"","distance":109870.7957133422}]

SAVED to scratchpad/stationsAndSatellites_1609499026969.csv:
Location,Name,Frequency,Duplex,Offset,Tone,rToneFreq,cToneFreq,DtcsCode,DtcsPolarity,Mode,TStep,Skip,Comment,URCALL,RPT1CALL,RPT2CALL,DVCODE
0,GB3CB,433.3500,split,434.9500,Tone,67,67.0,023,NN,FM,5.00,,,,,,
1,GB3BM,145.7125,split,145.1125,Tone,67.0,67.0,02
...SNIPPED...
,ISS-3,437.8,split,145.99,Tone,67,67.0,023,NN,FM,5.00,,,,,,
113,ISS-2,437.7975,split,145.99,Tone,67,67.0,023,NN,FM,5.00,,,,,,
114,ISS-1,437.795,split,145.99,Tone,67,67.0,023,NN,FM,5.00,,,,,,
115,ISS-0,437.7925,split,145.99,Tone,67,67.0,023,NN,FM,5.00,,,,,,
```

Suggested workflow for your radio:
- open CHIRP
- download from radio
- backup *.img file
- import the CSV
- load into default rows (or modify if you know what you're doing)
- save the *.img file
- upload to radio
- profit

## html

### repeaterMap.html

![alt text](/img/repeaterMapSample.png?raw=true)
<!-- ![alt text](https://github.com/m7xer/handy/blob/master/img/repeaterMapSample.png?raw=true) -->

Displays repeaters on an open street map in a way that is somewhat more printable than others.

Usage:

`
open html/repeaterMap.html  
`

Advanced usage:
paste the output from generateChirpCSV suitableRepeaters or allRepeaters json into the repeaters var at the bottom of repeaterMap.html, modify `center: [52.458333333333336, -1.9166666666666667]` at the top to see a custom view, save and refresh.

# TODO

- ~~csv generator for repeaters~~
- ~~offer ukrepeater info as json (can be found in allRepeaters json output from running generateChirpCSV)~~
- ~~printable local repeater map~~
- spit out a repeaterMap from generateChirpCSV
- allow for custom output folder for all the csv/json
- calendar with local net info
- generate elevation LOS graphs for repeaters using https://developers.google.com/maps/documentation/elevation/overview?hl=ru
- refactor so it's more maintainable, use ramda for neater list processing, make js adhere to [standard](https://www.npmjs.com/package/standard).
- grc files for various flows (maybe in a different sdr project)
