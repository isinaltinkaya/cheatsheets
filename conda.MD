#### Conda env using miniconda
See https://docs.conda.io/en/latest/miniconda.html

## - install conda

```
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh
```

## - turn-off auto init of conda env at startup
```
conda config --set auto_activate_base false
```


## - export the codna environment for later use

```
conda env export >> env.yml
```


For cross platform compatibility, use `--from-history` flag to only include packages that were explicitly installed instead of including every package in environment.

```
conda env export --from-history >> env.yml
```

## - create environment at a specific location
```
conda create --prefix ./envs
```
