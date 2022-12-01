## - conda speedup

- Disable safety checks
```
conda config --set safety_checks disabled
```

- Be more specific with versions
`numpy` -> `numpy=1.15` or even better `numpy=1.15.4`

- Specify particular R implementations
`r-essentials` -> `r-base=3.5 r-essentials`

- Eliminate possible mixed solutions:
```
conda config --set channel_priority strict
```

- Use mamba

See https://www.anaconda.com/blog/understanding-and-improving-condas-performance

## - install conda
Conda env using miniconda, see https://docs.conda.io/en/latest/miniconda.html

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


