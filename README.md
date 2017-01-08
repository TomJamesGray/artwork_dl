# Artwork DL
Program to download album artwork using the Musicbrainz and Cover art archive api

## Usage
```
usage: artwork_dl [-h] [--out OUT] [--quality QUALITY] artist album

positional arguments:
  artist
  album

optional arguments:
  -h, --help         show this help message and exit
  --out OUT          Specify output file, default cover.jpg
  --quality QUALITY  Specify desired quality: original,large or small
```

## Dependencies
* BeautifulSoup4
* Requests
* Wget for downloading the image
* ImageMagick for converting the image to a jpg if it's download as  a png, this should 
only occur if using the "original" image quality


## Examples
Download small (250px) cover art for "Bad Vibrations" by "A Day To remember" to file "cover_art.jpg" 

`artwork_dl "A Day To remember" "Bad Vibrations" --quality small --out cover_art.jpg`

---
Go through music directory (presuming it's structured by ARTIST/ALBUM) and download
the cover art for that album if it doesn't already exist
```
#!/bin/bash
base_dir=~/Music

for artist in */; do
  cd "$artist"
  for album in */; do
    cd "$album"
    if [ ! -f "cover.jpg" ]; then
      echo "$album"
      artwork_dl "$artist" "$album"
    fi
    cd ../
  done
  cd $base_dir
done
```
