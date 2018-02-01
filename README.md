# Artwork Extractor (awe)

awe can be used to extract artwork from mp3, m4a, ... audio files and save
it to a particular file ("sidecar file") in each folder.

I am using the Synology AudioStation to play music in my local environment
and found that AudioStation ignores many of the embedded cover artwork.
One solution to that is to extract the cover artwork and to save it as
`folder.jpg` or `cover.jpg` to the album's folder.

awe will do exactly that.

## Command line options

```sh
usage: awe [-h] [-a] [-r] [-f] [-n NAME] [-q | -v] [-s] [--dry-run]
           [dir [dir ...]]

awe extracts cover artwork from music files and saves it to a file in the each
album's directory.

positional arguments:
  dir                   Directory that contains the music files. If none
                        given, the current directory will be used.

optional arguments:
  -h, --help            show this help message and exit
  -a, --all-dirs        Usually only leaf directories (dirs that do not
                        contain other dirs) are processed. If you want to
                        process all directories and put sidecar files to it
                        you can specify this option.
  -r, --recursive       Dive into subdirectories. Useful if you want to use
                        awe for complete music collections.
  -f, --force           Overwrite already existing sidecar files.
  -n NAME, --name NAME  Name of the sidecar file to write in each folder that
                        contains media files with embedded album artwork.
                        Default is cover.jpg.
  -q, --quiet           Do not print anything to stdout but error messages.
  -v, --verbose         Be more verbose what happens.
  -s, --summary         Prints a summary after finishing the run.
  --dry-run             Do not write any cover artwork files to disk or change
                        anything else. This simulates a run and shows whats
                        going on.
```

## License
