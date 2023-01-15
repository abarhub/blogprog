+++
title = "Description of tar command"
date = "2022-09-08"
description = "Description of tar command"
tags = ["tar"]
summary = "Description of tar command"
+++
# Exemple de commandes Tar

```shell
# Deflate / Compress
$ tar -czf archive.tar.gz /path/files

# Inflate / Uncompress
$ tar -xzf archive.tar.gz

# Extract file to a defined directory
$ tar -xzf archive.tar.gz -C /target/directory

# Append a file to an existing archive
$ tar -zu archive.tar.gz -C /target/file
```

# Common options
* z :	compress with gzip
* c :	create an archive
* u :	append files which are newer than the corresponding copy ibn the archive
* f :	filename of the archive
* v :	verbose, display what is inflated or deflated
* a :	unlike of z, determine compression based on file extension
                    