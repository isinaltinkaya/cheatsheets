# Bash Cheatsheet

___

#### -> redirect stderr to stdout
`command 2>&1 | less`

___

### -> pass file list to copy
`cat filelist | xargs -I{} cp -u {} destination/`

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
  
[Credit](https://stackoverflow.com/questions/3601515/how-to-check-if-a-variable-is-set-in-bash)


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

  
  
  
 +--------------------+----------------------+-----------------+-----------------+
|   Expression       |       parameter      |     parameter   |    parameter    |
|   in script:       |   Set and Not Null   |   Set But Null  |      Unset      |
+--------------------+----------------------+-----------------+-----------------+
| ${parameter:-word} | substitute parameter | substitute word | substitute word |
| ${parameter-word}  | substitute parameter | substitute null | substitute word |
| ${parameter:=word} | substitute parameter | assign word     | assign word     |
| ${parameter=word}  | substitute parameter | substitute null | assign word     |
| ${parameter:?word} | substitute parameter | error, exit     | error, exit     |
| ${parameter?word}  | substitute parameter | substitute null | error, exit     |
| ${parameter:+word} | substitute word      | substitute null | substitute null |
| ${parameter+word}  | substitute word      | substitute word | substitute null |
+--------------------+----------------------+-----------------+-----------------+

+--------------------+----------------------+-----------------+-----------------+
|   Expression       |  FOO="world"         |     FOO=""      |    unset FOO    |
|   in script:       |  (Set and Not Null)  |  (Set But Null) |     (Unset)     |
+--------------------+----------------------+-----------------+-----------------+
| ${FOO:-hello}      | world                | hello           | hello           |
| ${FOO-hello}       | world                | ""              | hello           |
| ${FOO:=hello}      | world                | FOO=hello       | FOO=hello       |
| ${FOO=hello}       | world                | ""              | FOO=hello       |
| ${FOO:?hello}      | world                | error, exit     | error, exit     |
| ${FOO?hello}       | world                | ""              | error, exit     |
| ${FOO:+hello}      | hello                | ""              | ""              |
| ${FOO+hello}       | hello                | hello           | ""              |
+--------------------+----------------------+-----------------+-----------------+   +----------------------+------------+-----------------------+-----------------------+
   |   if VARIABLE is:    |    set     |         empty         |        unset          |
   +----------------------+------------+-----------------------+-----------------------+
 - |  ${VARIABLE-default} | $VARIABLE  |          ""           |       "default"       |
 = |  ${VARIABLE=default} | $VARIABLE  |          ""           | $(VARIABLE="default") |
 ? |  ${VARIABLE?default} | $VARIABLE  |          ""           |       exit 127        |
 + |  ${VARIABLE+default} | "default"  |       "default"       |          ""           |
   +----------------------+------------+-----------------------+-----------------------+
:- | ${VARIABLE:-default} | $VARIABLE  |       "default"       |       "default"       |
:= | ${VARIABLE:=default} | $VARIABLE  | $(VARIABLE="default") | $(VARIABLE="default") |
:? | ${VARIABLE:?default} | $VARIABLE  |       exit 127        |       exit 127        |
:+ | ${VARIABLE:+default} | "default"  |          ""           |          ""           |
   +----------------------+------------+-----------------------+-----------------------+
+----------------------+-------------+---------+------------+
| Expression in script | name='fish' | name='' | unset name |
+----------------------+-------------+---------+------------+
| test "${name+x}"     | TRUE        | TRUE    | f          |
| test "${name-x}"     | TRUE        | f       | TRUE       |
| test -z "$name"      | f           | TRUE    | TRUE       |
| test ! "$name"       | f           | TRUE    | TRUE       |
| test ! -n "$name"    | f           | TRUE    | TRUE       |
| test "$name" = ''    | f           | TRUE    | TRUE       |
+----------------------+-------------+---------+------------+
