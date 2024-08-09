### paste icon unicode

```
> go to insert mode
> ctrl+v
> enter letter 'u'
> write the unicode of the icon (e.g. f0133)
```


### reuse match

test1 to output/test1

test2 to output/test2

```
:%s/test\(.\)$/output\/test\1/g
```



array[1] to a1

array[2] to a2


```
:s/(array)\[([1-9])\]/a\2/g
```
