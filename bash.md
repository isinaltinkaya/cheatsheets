# Bash Cheatsheet

___

#### -> redirect stderr to stdout
`command 2>&1 | less`

___

### -> pass file list to copy
`cat filelist | xargs -I{} cp -u {} destination/`

___

### -> check if variable is set

If you want `var=''` to be evaluated as var is set;
```
if [ -z ${var} ]; then echo "var is unset"; else echo "var is set to '$var'";fi
```

If you want `var=''` to be evaluated as var is unset;
```
if [ -z ${var+x} ]; then echo "var is unset"; else echo "var is set to '$var'";fi
```

[credit](https://stackoverflow.com/a/13864829/7870777)

___


### -> prefer `mapfile` `read-a` or quotes
[credit: mostly copy paste](https://github.com/koalaman/shellcheck/wiki/SC2207)


Unquoted command expansion in an array invokes the shell's sloppy word splitting and glob expansion:
```
##BAD
array=( $(mycommand) ) 
```
Instead, prefer explicitly splitting (or not splitting).

If you want to split the output into lines or words, use `mapfile`, `read -ra` and/or `while loops`.
```
# For bash 4.x, must not be in posix mode, may use temporary files
mapfile -t array < <(mycommand)

# For bash 3.x+, must not be in posix mode, may use temporary files
array=()
while IFS='' read -r line; do array+=("$line"); done < <(mycommand)

# For ksh, and bash 4.2+ with the lastpipe option enabled (may require disabling monitor mode)
array=()
mycommand | while IFS="" read -r line; do array+=("$line"); done
```


If it outputs a line with multiple words (separated by spaces), other delimiters can be chosen with IFS, each of which should be an element:

```
# For bash, uses temporary files
IFS=" " read -r -a array <<< "$(mycommand)"

# For bash 4.2+ with the lastpipe option enabled (may require disabling monitor mode)
array=()
mycommand | IFS=" " read -r -a array

# For ksh
IFS=" " read -r -A array <<< "$(mycommand)"
```


If the output should become a single array element, quote it:
```
array=( "$(mycommand)" )
```

This prevents the shell from doing unwanted splitting and glob expansion, and therefore avoiding problems with output containing spaces or special characters.


___

| expression | `FOO='V'`    | `FOO=''`     | `unset FOO`  |
|------------|------------|------------|------------|
| `${FOO:-x}`  | V          | x          | x          |
| `${FOO-x}`   | V          |            | x          |
| `${FOO:=x}`  | V          | x          | x          |
| `${FOO=x}`   | V          |            | x          |
| `${FOO:?x}`  | V          | <error>    | <error>    |
| `${FOO?x}`   | V          |            | <error>    |
| `${FOO:+x}`  | x          |            |            |
| `${FOO+x}`   | x          | x          |            |
  


|   if VARIABLE is:    |    set     |         empty         |        unset          |
| -- | -- | -- | --
| - |  ${VARIABLE-default} | $VARIABLE  |          ""           |       "default"       |
|  = |  ${VARIABLE=default} | $VARIABLE  |          ""           | $(VARIABLE="default") |
|  ? |  ${VARIABLE?default} | $VARIABLE  |          ""           |       exit 127        |
|  + |  ${VARIABLE+default} | "default"  |       "default"       |          ""           |
| :- | ${VARIABLE:-default} | $VARIABLE  |       "default"       |       "default"       |
| := | ${VARIABLE:=default} | $VARIABLE  | $(VARIABLE="default") | $(VARIABLE="default") |
| :? | ${VARIABLE:?default} | $VARIABLE  |       exit 127        |       exit 127        |
| :+ | ${VARIABLE:+default} | "default"  |          ""           |          ""           |

  
  
  
| Expression in script: | parameter [Set and Not Null] | parameter [Set But Null] | parameter [Unset] |
|--------------------|----------------------|-----------------|-----------------|
| ${parameter:-word} | substitute parameter | substitute word | substitute word |
| ${parameter-word}  | substitute parameter | substitute null | substitute word |
| ${parameter:=word} | substitute parameter | assign word     | assign word     |
| ${parameter=word}  | substitute parameter | substitute null | assign word     |
| ${parameter:?word} | substitute parameter | error, exit     | error, exit     |
| ${parameter?word}  | substitute parameter | substitute null | error, exit     |
| ${parameter:+word} | substitute word      | substitute null | substitute null |
| ${parameter+word}  | substitute word      | substitute word | substitute null |

  
| Expression in script: |  FOO="world"  [Set and Not Null] | FOO=""  [Set But Null] | unset FOO [Unset] |
|--------------------|----------------------|-----------------|-----------------|
| ${FOO:-hello}      | world                | hello           | hello           |
| ${FOO-hello}       | world                | ""              | hello           |
| ${FOO:=hello}      | world                | FOO=hello       | FOO=hello       |
| ${FOO=hello}       | world                | ""              | FOO=hello       |
| ${FOO:?hello}      | world                | error, exit     | error, exit     |
| ${FOO?hello}       | world                | ""              | error, exit     |
| ${FOO:+hello}      | hello                | ""              | ""              |
| ${FOO+hello}       | hello                | hello           | ""              |

  
|   if VARIABLE is:    |    set     |         empty         |        unset          |
--------------------|----------------------|-----------------|-----------------|
| - |  ${VARIABLE-default} | $VARIABLE  |          ""           |       "default"       |
| = |  ${VARIABLE=default} | $VARIABLE  |          ""           | $(VARIABLE="default") |
| ? |  ${VARIABLE?default} | $VARIABLE  |          ""           |       exit 127        |
| + |  ${VARIABLE+default} | "default"  |       "default"       |          ""           |
| :- | ${VARIABLE:-default} | $VARIABLE  |       "default"       |       "default"       |
| := | ${VARIABLE:=default} | $VARIABLE  | $(VARIABLE="default") | $(VARIABLE="default") |
| :? | ${VARIABLE:?default} | $VARIABLE  |       exit 127        |       exit 127        |
| :+ | ${VARIABLE:+default} | "default"  |          ""           |          ""           |

  
  | Expression in script | name='fish' | name='' | unset name |
|--------------------|----------------------|-----------------|-----------------|
| test "${name+x}"     | TRUE        | TRUE    | f          |
| test "${name-x}"     | TRUE        | f       | TRUE       |
| test -z "$name"      | f           | TRUE    | TRUE       |
| test ! "$name"       | f           | TRUE    | TRUE       |
| test ! -n "$name"    | f           | TRUE    | TRUE       |
| test "$name" = ''    | f           | TRUE    | TRUE       |

  
[Credit](https://stackoverflow.com/questions/3601515/how-to-check-if-a-variable-is-set-in-bash)

  
  ____
  
  
| Syntax	| Result |
| -- | -- |
arr=()	| Create an empty array
arr=(1 2 3)	| Initialize array
${arr[2]}	|	Retrieve third element
${arr[@]}	|	Retrieve all elements
${!arr[@]}	|	Retrieve array indices
${#arr[@]}	|	Calculate array size
arr[0]=3	|	Overwrite 1st element
arr+=(4)	|	Append value(s)
str=$(ls)	|	Save ls output as a string
arr=( $(ls) )	|	Save ls output as an array of files
${arr[@]:s:n}	|	Retrieve n elements starting at index s

  [Credit](https://opensource.com/article/18/5/you-dont-know-bash-intro-bash-arrays)

  
  
---
  
##Change output seperator properly

Use `echo $(cat file)` instead of `cat file`

Instead of this:
```
$ cat sim2/model_OutOfAfrica_3G09/contig_chr22/sfs/sim2-OutOfAfrica_3G09-chr22-rep3-d2_indpair_pop2_ind45-pop3_ind25.sfs| tr ' ' ','
130401.839417,5204.746850,860.006540,7636.679624,2810.368398,4270.813548,819.873691,1719.716788,4978.955144,
```

You get this:
```
$ echo $(cat sim2/model_OutOfAfrica_3G09/contig_chr22/sfs/sim2-OutOfAfrica_3G09-chr22-rep3-d2_indpair_pop2_ind45-pop3_ind25.sfs)| tr ' ' ','                                                                    
130401.839417,5204.746850,860.006540,7636.679624,2810.368398,4270.813548,819.873691,1719.716788,4978.955144
```

---



```  
$ cat file.txt
a
b
c
$ paste -s -d ',' file.txt 
a,b,c
```
