# FM-Adaptive

## What is it?
  	 FM-Adaptive is a full-text compressed index and combines the Burrows-Wheeler transform (BWT)
	 and the wavelet tree (WT).  It partitions adaptively the node bit vector in the WT into blocks
	 and applies the hybrid encoding along with run-length Gamma encoding to each block while
	 explores data-aware compression. It retains the high-order entropy-compressed theoretical
	 performance and introduces some improvements in practice. Statistical evidence shows that
	 the distribution of run-lengths for the non-repetitive data appears to follow a power-law
	 distribution, which matches the optimality of the Gamma encoding to the run-lengths.
	 
	 counting: compute the number of occurrences of pattern P in the text T.
	 locating: report the list of positions, where P occurs in T.
	 extract: extraction of arbitrary portions of T.

## How to use it?
### just for fun
 step 1: download it or clone it  
 step 2: make  
 step 3: run my_fm  

### build your own program
 step 1: download or clone it  
 step 2: make   
 step 3: include FM.h   
 step 4: g++ your_program.cpp -o xx -fm.a   

### example
```cpp
#include "fm.h"
#include <iostream>
using namespace std;
int main()
{
    int speedlevel = 1;
    FM fm("filename", speedlevel); //default speedlevel = 1
    int num;
    fm.Counting("the", num);
    cout << "pattern the occs " << num<< " times" <<endl;
    int *pos;
    fm.Locating("love", num,pos);
    cout << "pattern love occs " << num<< " times" << endl;
    cout << "all the positions are:";
    for (int i = 0; i < num; i++)
        cout << pos[i] << endl;
    delete [] pos; //it's your duty to delete pos.
    pos = NULL;

    char * sequence;
    int start = 0;
    int len = 20;
    fm.Extracting(start, len, sequence);
    cout << "T[start...start+len-1] is " << sequence << endl;
    delete [] sequence; //it's your duty to delete sequence.
    sequence = NULL;

    fm.Save("index.fm"); //serialize the fm object to file index.fm
    FM fm2;
    fm2 -> Load("index.fm"); //restore the fm object from file index.fm

    return 0;
}
```
## Suffix Array Construction
  The current version uses Yuta Mori's fast suffix array construction library [libdivsufsort](http://code.google.com/p/libdivsufsort/) version 2.0.1.

