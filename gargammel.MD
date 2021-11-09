# gargammel


# 1. Simulate degradation

Gargammel uses`fragSim.cpp` to simulate the fragmentation using the input sequence. Available options are:

 ```
                -l      [length]                Generate fragments of fixed length  (default: 35)
                -s      [file]                  Open file with size distribution (one fragment length per line)
                -f      [file]                  Open file with size frequency in the following format:
                                                length[TAB]freq ex:
                                                40      0.0525
                                                41      0.0491
 ```
 According to the definitions used in Gargammel, fragment length is the length of our real fragment before adding any adapter etc.

 

If you define a fragment size distribution `-s` or a fragment size frequency distribution `-f`, this overwrites the fraglength variable which is 35 by default.
  `-f sizefreq.size.gz`

 
`fragSim.cpp` uses the fragment size distribution to calculate cumulative probabilities, and draws fragment lengths to simulate accordingly. This is exactly where this happens: https://github.com/grenaud/gargammel/blob/da98a1884c40d8869eb15fa275d4b0ddd74c8bab/src/fragSim.cpp#L152-L174


# 2. Simulate damage

`deamSim.cpp`



# 3. Add adapters

`adptSim.cpp`
This simulates the adapters using the following logic:
For each fragment,
- If your fragLength<readLength it will add adapter sequence. Else it will not add any adapters.

Therefore, if your size frequency distribution has reads <75bp, some of your reads should have adapters.

If you used the one gargammel provides, it allows <75bp:
```
Sizefreq.size.gz:
35      0.00540914
36      0.00785707
37      0.00921923
38      0.0119435
39      0.0146481
40      0.017096
41      0.01832
…
```
 
- If fragLength+adapter is still <readLength, it will add random bases to the end.
This process I explained above happens here:
https://github.com/grenaud/gargammel/blob/da98a1884c40d8869eb15fa275d4b0ddd74c8bab/src/adptSim.cpp#L294-L323
 
# 4. Run Illumina art program to simulate the sequencing

Read length is fixed, it is the read length that will be ‘sequenced’. The default value for this is 75:
```
-rl    [length]           Desired read length  (Default: 75)
``` 
And by default, this is the sequencing platform it will use:
```
HS25 - HiSeq 2500        Paired end max. read length: 150bp 
```
Therefore you can’t define any read length >150bps using this platform, if you want to do so you need to change the sequencing platform.

---

# Output files

As output:

In data directory,

`OUT.e.fa.gz` : Reads coming from fragSim

`OUT_d.fa.gz` : Reads coming from deamSim

`OUT_a.fa.gz` : Reads coming from adptSim. These are the reads with the adapters ligated on the deaminated fragments.
 
If you compare e.fa.gz with a.fa.gz you should see the difference and understand whether if you have adapters. But if you need to know if you have adapters, you can use -name option with adptSim.cpp (https://github.com/grenaud/gargammel/blob/da98a1884c40d8869eb15fa275d4b0ddd74c8bab/src/adptSim.cpp#L77) 
When you use this option, it will add following identifiers:

```
AD = added adapter
RD = added random
```

as defined in 
https://github.com/grenaud/gargammel/blob/da98a1884c40d8869eb15fa275d4b0ddd74c8bab/src/adptSim.cpp#L347-L350
