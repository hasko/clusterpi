# clusterpi

Stuff to remember when setting up the Raspbian image:

* Add a file called `ssh` in the boot partition. Otherwise the Pi isn't reachable with `ssh`.
* Edit the file `commandline.txt` in the boot partition and remove the `init=expandsomthingwhatever`. Otherwise the file system will be expanded automatically upon first boot, leaving no room for the GlusterFS filesystem (which shouldn't be on the root partition).
* Upon first boot, grow the root partition and create an additional partition for the GlusterFS file system with `parted`.
* Resize the file system with `sudo resize2fs /dev/mmcblk0p2`.
* Install XFS tools: `apt-get install xfsprogs`
* `mkfs.xfs -i size=512 /dev/mmcblk0p3` must be done manually because it's dangerous.
* Authorize `ssh` from Ansible master.
  * `ssh b@B mkdir -p .ssh`
  * `cat .ssh/id_rsa.pub | ssh b@B 'cat >> .ssh/authorized_keys'`
