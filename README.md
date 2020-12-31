# handy
utilities for handheld radio

## install

`
npm install
`

## scripts

### generateChirpCSV

Generate CSV for CHIRP programming, with the 60 most local UK repeaters and a bunch of satellites with Doppler adjusted downlinks.

Usage:
Pass in your UK [Maidenhead locator](https://www.levinecentral.com/ham/grid_square.php) to obtain the nearest 2M and 70CM analogue voice repeaters for you. Satellite data will be augmented before the final CSV is generated. Modify the script for more features as YMMV!

`
./scripts/generateChirpCSV IO92BL
`

Output:
.json and .csv files will be output. Suggested workflow for your radio:
- open CHIRP
- download from radio
- backup *.img file
- import the CSV
- load into default rows (or modify if you know what you're doing)
- save the *.img file
- upload to radio
- profit

# TODO

- ~~csv generator for repeaters~~
- offer ukrepeater info as json (can be found in allRepeaters output from generateChirpCSV)
- printable local repeater map
- calendar with local net info
- generate elevation LOS graphs for repeaters using https://developers.google.com/maps/documentation/elevation/overview?hl=ru
- grc files for various flows (maybe in a different sdr project)
