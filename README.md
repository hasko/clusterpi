# clusterpi

Stuff to remember when setting up the Raspbian image:

* Add a file called `ssh` in the boot partition. Otherwise the Pi isn't reachable with `ssh`.
* Edit the file `commandline.txt` in the boot partition and remove the `init=expandsomthingwhatever`. Otherwise the file system will be expanded automatically upon first boot, leaving no room for the GlusterFS filesystem (which shouldn't be on the root partition).
* Upon first boot, grow the root partition and create an additional partition for the GlusterFS file system.
* `mkfs.xfs` must be done manually because it's dangerous.
