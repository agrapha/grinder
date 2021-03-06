grinder
=======

An After Effects "aerender" front end that supports watch folder style rendering for primarily frame based projects

This version of the script was used successfully in production across 8 workstations, each with 3-5 instances of aerender running. This was in full production for AE CC in 2013.

More info and some associated tools still to come. If you want more info or to use this, contact me here

Rendering with Grinder For Mac Workstations Only
==========================================
For the macs in production we have developed a script called grinder that enables After Effects to render using the aerender module instead of a GUI copy of After Effects (AE). The script utilizes existing AE watchfolder collecting tools to speed up processing of AE projects - both on a single machine and with multiple machines.

USE:

1. Open the Terminal application and type:

```
grinder -n 2 -w path/to/the/watchfolder
```

the number 2 can be replaced with other numbers and represents the number of aerender insqances that will be started on this machine. It is safe to use n = 1/2 of the number of cores on your machine if you will ONLY be rendering.

Note: it is possible to continue working in AE while you let grinder watch a folder. If you need to keep working use a low number of instances so that your machine does not bog down.

the path to the watchfolder can be on a network volume but all machines attempting to render must have access to all the necessary files (this is similar to a watchfolder render)

to stop grinder from running, use control-C in the terminal window where it is running.

OTHER INFO:
===========
Grinder works in cooperation with Watch Folder renders so it should be possible to use them both at the same time. Grinder will not pick up a project that has been completed by a watch-render and it sets stop files that will keep watch renders from starting after grinder has run successfully.

There are logs kept for each individual instance of aerender running on every machine in the “Grinder Logs” folder that is along side the rendered project file. Using these you can track frame problems back to an individual machine and there is a script available to delete all frames rendered by that instance (more info to come here)

WARNINGS
========
grinder is expected to fail for all except 1 instance when rendering a movie. Grinder works best with frame renders that are set up to optimize for skip-frame rendering (similar to the watch folder). If you need to include movie files in your project be aware that multiple machines will NOT work on the render and if there are movies before other frames in the Render Queue of the project, you will end up with only one instance working on everything after the movie.

Every effort has been made to have grinder clean up bad dpx frames after a render but if you are rendering to other formats there may be small or zero-size frames left behind if grinder is quit early, or if it crashes.

INSTALLATION
============
To install grinder you must make a copy of the master file into the /opt/local/bin directory of a properly set up workstation. The file should have the ”.py” extension removed and the mode for the file set to executable (chmod a+x grinder)

Note that the /opt/local/bin directory is installed by MacPorts as part of the new machine set up process - this also installs the correct version of Python necessary to run the script. Install grinder AFTER the procedures in the IT section are followed.

If you are installing without macports you should use python 2.6 or 2.7 and you can put the executable in any system PATH accessible location.
