# xnor

This challenge gave two files `xnor.py` and `xnor_output.txt`
>XNOR! It's like XOR, but it's actually the complete opposite.

First I checked the `xnor.py` file:
```

```

I saw that the program generated a random key, and then xnor encrypted the message `b"Blue is greener than purple for sure!"`  
It printed the result, and then xnor encrypted the flag as well.  

I know with xor and xnor encryption that the output can be encrypted with one of the inputs to get the other input.  
If I have the given input encrypted before the flag, as well as its output after decryption,  
I can get the key that is used to encrypt the flag. Both the input and outputs were in `xnor_output.txt`:
'''

'''

I looked up an xnor tool online and put in this example to get the flag.  
Then I used this with the output for the flag encryption in `xnor_output.txt` to get the flag:

`}3v15ulcx3_os_gn13b_u0y_r0nx_yhw{ftcb`

This looked like the flag backwards, so I reversed it:

```
$ rev }3v15ulcx3_os_gn13b_u0y_r0nx_yhw{ftcb
bctf{why_xn0r_y0u_b31ng_so_3xclu51v3}
```
