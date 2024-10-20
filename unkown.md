#unkown
>Some may call this junk. Me, I call them treasures.

This challenge gave me a file `unknown.zip'

I decided to analyze what type of file this is:
```
file unkwnown.zip
unknown.zip: gzip compressed data, from Unix, original size modulo 2^32 10240
```

I see that the file is a gzip file, not a zip. I renamed the file to unknown.gz, and upon opening it found flag.txt
```
cat flag.txt
bctf{f1l3_3x73n510n5_4r3_n07_r341}
```
