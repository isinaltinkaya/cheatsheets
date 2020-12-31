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

