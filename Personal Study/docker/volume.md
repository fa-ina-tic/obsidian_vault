
![[Pasted image 20231218091900.png]]

preferred mechanism for persisting data which is generated and used in docker container.

## volume vs [[bind mount]]
[[bind mount]]s are dependent on the directory structure and OS of the host machine, volumnes are completely managed by docker
volume doesn't increase the size of container
### Volume's advantage over bind mounts
1. easier to backup or migrate
2. Can manage volumes using docker CLI or docker API
3. Can use in linux & window containers 
4. can be more safely shared among multiple containers

## --mount vs -v
--mount is more explicit and verbose.
-v combines all the options together in one field and --mount seperates them
--mount flag
1. type : bind, volume, tmpfs
2. source : name of the volume
3. destination : where the file or directory is mounted in the container
4. readonly: readonly or ro
5. volume-opt : key-value pair of option name and value
