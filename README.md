# Using-the-glob-module
This repository explains how to use the Glob standard library module to produce a list of pathnames that match a specific file extension pattern.

#About glob
glob is a module from the Python standard library that provides a means for searching through sub-folders of a directory and only using the files that are needed. In the case of having a directory with sub-folders full of files with different Unix shell extensions (such as mp3, text, py), a list of all the mp3 file names in the directory could be produced by passing glob the ".mp3" pattern. This module serves to be very useful as it eliminates the need to move files around, and generates a list of all the files needed by a given script. As a result whenever the data in those files needs to be used, all the files will be acessible via traversing the list of filenames as opposed to having to walk the tree of files from the root and pass over files that are not needed. In this way the glob module greatly increases the performance of a script by making it to where the entire tree of files in sub-folders of a directory only needs to be traversed once as opposed to needing to be traversed with multiple times.

#How I used glob
For a world music map project I have been working on recently I needed a way to efficiently obtain information about a given song's: artist, title, longitude, and latitude, and I had a myriad of files to go through. The Million Song Database (MSD) is a vast music database produced by EchoNest which provides meta-data for around a million songs. I was using a 10,000 song sample set from the much larger MSD because I wanted to work on a much smaller scale. The sample set was in a folder that had two different sub-levels of sub-folders which meant that quickly getting to all of the h5 files within the directory would be a difficult task, but then I came across glob. With the use of the glob module I was able to promptly link all of the h5 files in the sample set path together into a list so that I could then index them one by one and extract the artist, title, longitude and latitude data from the song. A process that could have taken minutes to complete was done in the matter of seconds by incorporating the use of glob (specifically the glob() function) into my script.

#Resource to tell you more about glob
[glob](https://docs.python.org/2/library/glob.html)

#Usage
Need to import:
glob
os

Glob works with a couple different functions from the built-in Python operating system modules which is why you have to import os as well. Glob uses walk() in order to traverse all folders and sub-folders within the directory, then  calls to path() and join() in concordance to link the path between all of the extension specific files. Join() essentially connects the links from the root of the directory tree all the way down to the leaves, based on the file extension passed to the function. Glob then performs the action of placing each file name into an index of the list that will result in being the list of all file names upon glob finishing execution.

```
def getTrackData(basedir,ext='.h5'):
        trackList = []
        count = 0
        for root, dirs, files in os.walk(basedir):
                files = glob.glob(os.path.join(root,'*'+ext))
                for file in files:
```
Above is an example of how I used glob in my script. Once the for loop is reached, the list "files" has been populated with the names of all of the files in the given base directory (basedir) matching the provided .h5 extension specifier. With the filename list filled I was then able to begin retreiving the data I needed from those files.
