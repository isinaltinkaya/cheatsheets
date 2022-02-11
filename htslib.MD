# HTSLIB related stuff


### Add htslib as submodule
```
git submodule add https://github.com/samtools/htslib.git
git submodule update --init --recursive #get htslib/htscodecs submodule of htslib
cd htslib
git checkout c37e0413d42b47328c94a5f21814526de5d2312e #latest major release hash
```

