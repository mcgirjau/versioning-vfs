# Versioning Virtual File System

An implementation of a versioning virtual file system using FUSE

This VFS implementation splits the `stg` directory into two subdirectories: 
`storage` and `versions`. The `mnt` directory has been set to only mirror the
`stg/storage` directory, while the versions themselves are saved in `stg/versions`.
This way, version files are not visible or accessible from within `mnt`, and
the version dump process becomes a relatively easy endeavor.

All versions of a particular file, named for example `filename.ext`, can be 
accessed by looking into the `stg/versions` directory, from any location in or 
outside of the file system.

So then to dump all of the file versions for `filename.ext` into the current
directory, one can run the following terminal command:

```{sh}
find path/to/stg/versions -name "*" | grep -E "filename\.ext,[0-9]+$" | xargs cp -t .
```

Specifically from within the `sysproj-8` root project directory, the above command
can be simplified as:

```{sh}
find stg/versions -name "*" | grep -E "filename\.ext,[0-9]+$" | xargs cp -t .
```
