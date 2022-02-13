# ANGSD Contribution Cheatsheet

### - Base lookup table (refToInt intToRef)

```
char majorC = intToRef[pars->major[s]];
char minorC = intToRef[pars->minor[s]];
```

intToRef | <maps_to>
| -- | -- |
0 | a
0 | A
1 | c
1 | C
2 | g
2 | G
3 | t
3 | T
4 | n
5 | N




```
typedef struct  tNode_t{//order is important. First 8 bytes will be modified by pool_alloc structure (James Bonfield)
  int l;//4
  int l2;//4//length of "insert"
  int refPos;//4
  int m;//4
  int m2;//4//possible length of insert before realloc
  char *seq;//8
  unsigned char *qs;//8
  suint *posi;//16
  suint *isop;//16
  unsigned char *mapQ;//8
  tNode_t **insert;//8 an insertion 8bytes;
  int deletion;//4 //counter
  unsigned char *rgs;//<- added 19july 2020 for keeping track of readgroups
}tNode;
```

```
chunkyT *chk = pars->chk;

// s = site_i [int s=0;s<pars->numSites;s++]
// i = ind_i [int i=0;i<pars->nInd;i++]
tNode *nd = chk->nd[s][i]


// how many reads per site per individual
nd->l [int]


```



```
typedef struct{
  int refId;
  int regStart;
  int regStop;
  int nSites;
  int nSamples;
  tNode ***nd;//nd[site][ind]
  int *refPos;//length is nSites
}chunkyT;
```


```
typedef struct {

  //primitives
  int chunkNumber; //4
  int numSites; //8
  int nInd; //12


  int refId;//reference number from header //16
  int *posi;//position is 0 indexed //24

  suint **counts;// contains counts of A,C,G,T //32 
  double **likes;// contains logscaled likelihoodratios, 10 per sample //40
  double **post;// contains genotype posteriors, 3 persample DRAGON //48
  
  char *major;//major //
  char *minor;//minor
  char *ref;//reference
  char *anc;//ancestral
 
  //sites removed in analysis and print
  int *keepSites;
  
  //stuff needed for bamreader
  fcb *for_callback;
  chunkyT *chk;
  int killSig;
  
  //extra stuff associated with each analysis module
  void **extras;
  
}funkyPars;
```
