# xnor

This challenge gave two files `xnor.py` and `xnor_output.txt`
>XNOR! It's like XOR, but it's actually the complete opposite.

First I checked the `xnor.py` file:
```
import os


def xnor_bit(a_bit, b_bit):
    if a_bit == "1" and b_bit == "1":
        return "1"
    elif a_bit == "1" and b_bit == "0":
        return "0"
    elif a_bit == "0" and b_bit == "1":
        return "0"
    elif a_bit == "0" and b_bit == "0":
        return "1"


def xnor_byte(a_byte, b_byte):
    a_bits = get_bits_from_byte(a_byte)
    b_bits = get_bits_from_byte(b_byte)

    result_bits = [xnor_bit(a_bits[i], b_bits[i]) for i in range(8)]
    result_byte = get_byte_from_bits(result_bits)
    return result_byte


def xnor_bytes(a_bytes, b_bytes):
    assert len(a_bytes) == len(b_bytes)

    return bytes([xnor_byte(a_bytes[i], b_bytes[i]) for i in range(len(a_bytes))])


def get_bits_from_byte(byte):
    return list("{:08b}".format(byte))


def get_byte_from_bits(bits):
    return int("".join(bits), 2)


message = b"Blue is greener than purple for sure!"
key = os.urandom(37)

flag = b"bctf{???????????????????????????????}"


def main():
    print(f"Key: {key.hex()}")
    print(f"\nMessage: {message}")

    encrypted = xnor_bytes(message, key)
    print(f"Enrypted message: {encrypted.hex()}")

    print(f"\nFlag: {flag}")
    encrypted_flag = xnor_bytes(flag, key)
    print(f"Encrypted flag: {encrypted_flag.hex()}")


if __name__ == "__main__":
    main()
```

I saw that the program generated a random key, and then xnor encrypted the message `b"Blue is greener than purple for sure!"`  
It printed the result, and then xnor encrypted the flag as well.  

I know with xor and xnor encryption that the output can be encrypted with one of the inputs to get the other input.  

If I have the given input encrypted before the flag, as well as its output after decryption,  
I can get the key that is used to encrypt the flag. Both the input and outputs were in `xnor_output.txt`:

```
Key: [[REDACTED]]

Message: b'Blue is greener than purple for sure!'
Enrypted message: fe9d88f3d675d0c90d95468212b79e929efffcf281d04f0cfa6d07704118943da2af36b9f8

Flag: [[REDACTED]]
Encrypted flag: de9289f08d6bcb90359f4dd70e8d95829fc8ffaf90ce5d21f96e3d635f148a68e4eb32efa4
```

I looked up an xnor tool online and put in this example to get the flag.  
Then I used this with the output for the flag encryption in `xnor_output.txt` to get the flag:

`}3v15ulcx3_os_gn13b_u0y_r0nx_yhw{ftcb`

This looked like the flag backwards, so I reversed it:

```
$ rev }3v15ulcx3_os_gn13b_u0y_r0nx_yhw{ftcb
bctf{why_xn0r_y0u_b31ng_so_3xclu51v3}
```
