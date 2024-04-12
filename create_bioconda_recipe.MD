# Create a new bioconda recipe


## 1- Fork bioconda recipes github repo


## 2-

```
git clone git@github.com:isinaltinkaya/bioconda-recipes.git
cd bioconda-recipes
git remote add upstream git@github.com:bioconda/bioconda-recipes.git
git checkout master
git pull upstream master
git push origin master
git checkout -b vcfgl
```

```
cd recipes
mkdir vcfgl
cd vcfgl
touch meta.yaml
touch build.sh
```

`build.sh`
```
```

`meta.yaml`

```
```


```
# get_sha
name=vcfgl
version=v1.0.0
username=isinaltinkaya
pass=${1}
url=$(curl -s https://api.github.com/repos/$username/$name/releases/latest -u $username:${pass}| jq -r '.assets[].browser_download_url');
wget -O- $url | shasum -a 256  > shasum256.txt
```


## 3- Test locally

```
conda create -n bioconda -c conda-forge -c bioconda bioconda-utils
conda activate bioconda
```


```
cd bioconda-recipes
bioconda-utils build  --packages vcfgl  --force --logfile ../vcfgl_build.log
```






