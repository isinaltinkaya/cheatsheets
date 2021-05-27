`set -e`
If a command fails, make the script exit; not continue with the next line.
If it is ok for one foo command to fail, use `false || foo`

`set -u`
If unset variable exists; exit

`set -f`
Disable globbing

`shopt -s failglob`
Use globbing but if a globbing fails give error
[details](https://www.gnu.org/software/bash/manual/html_node/The-Shopt-Builtin.html)

`set -o pipefail`
Fail pipeline if any command exits with error

```
set -euo pipefail
shopt -s failglob
```

Use "$var" instead of $var.
```
var="*.csv"
-> echo $var
test1.csv test2.csv
-> echo "$var"
*csv
```

$* ->not safe
$@ ->not safe
"$@" ->safe
[details](https://www.gnu.org/software/bash/manual/html_node/Special-Parameters.html)

[Use ShellCheck!!](https://www.shellcheck.net/)




## WRONG way to loop in a file
```
for line in $(cat myFile.txt); do echo "$line"; done
```
## CORRECT way
```
while read -r line; do echo "$line"; done < myFile.txt
```
## Another CORRECT way using mapfile builtin command
```
mapfile -t myArray < myFile.txt
for line in "${myArray[@]}"; do echo "$line"; done
```


## BAD practice: Returns globbing pattern when no file found
```
$for file in tmp/* tmp3/*; do echo $file; done
tmp/file1
tmp/file2
tmp/tmp2
tmp3/*
```

## BEST practice
```
for file in tmp/* tmp3/*; do { [[ -e $file ]] || continue; echo $file; } done
```

to prevent tools to spend lots of time treating your ascii (plain text) file as unicode: start script with `export LANG=C` 

use `export LC_ALL=C` to produce consistent ordering


use fail fast:
https://dougrichardson.us/notes/fail-fast-bash-scripting.html
