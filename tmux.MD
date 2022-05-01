## Kill frozen tmux if nothing else works

```
pkill -9 tmux
```
## If systemwide tmux installation is not available

```
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh
conda install -c conda-forge tmux
```
