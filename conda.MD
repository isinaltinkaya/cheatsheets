#### Conda env using miniconda
See https://docs.conda.io/en/latest/miniconda.html


```
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh
```

- turn-off auto init of conda env at startup
```
conda config --set auto_activate_base false
```

```
conda env export --from-history >> env.yml
```

### create at a specific loc
```
conda env create --prefix ./envs
```
