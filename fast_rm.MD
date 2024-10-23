Removing miniconda3/ takes too much time.

Solution1: perl (fastest)

```
perl -MFile::Find -MFile::Path=rmtree -e 'find(sub{unlink if -f && (stat)[9] < time}, "."); finddepth(sub{rmtree($_) if -d && $_ ne "."}, ".");'
```

Solution2: 

```
mkdir empty_dir
rsync -a --delete empty_dir/ miniconda3/
```

