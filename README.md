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

## Speed

I did not conduct a lot of tests but I was wondering if it is better to run
awe on a locally stored iTunes music database or run it directly on a NAS.
My local iTunes media library is stored on a SSD while the NAS uses six
5400-rpm disks in RAID6. The NAS is connected via cable using a 2 x 1 GBit
bond interface to my Mac Pro (macOS High Sierra). Both volumes are encrypted.

### Local SSD
```sh
fallenbeck@kafka:~/src/awe [master] $ ./awe -a -r -f -v -s /Volumes/Media/iTunes/iTunes\ Media/Music/
Found 2764 dir(s)

     Time elapsed:    194.016 secs
    Total folders:   2764
    Files written:   1438
    Files skipped:      0
Files not written:   1326
```

### NAS RAID6 on 6 5400-rpm HDDs
```sh
fallenbeck@kafka:~/src/awe [master] $ ./awe -a -r -f -v -s /Volumes/music/
Found 2764 dir(s)

     Time elapsed:    320.512 secs
    Total folders:   2764
    Files written:   1439
    Files skipped:      0
Files not written:   1325
```

I was a bit surprised that the runtime on the NAS is not that bad. Of course
it's a bit slower than working on a local SSD but it does not even need the
double amount of time. I expected the runtime on the NAS to be much worse.

## Known issues
**None**

## Remove all existing sidecar files from your library
If you want to remove all existing sidecar files from your library, you can
use a simple `find` command:

```sh
find /path/to/your/library/ -name "cover.*" -delete
```

If you use a different sidecar file name than `cover` you need to modify this
command.

## License

The software is licensed under the MIT license.

Copyright 2018 Niels Fallenbeck

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.