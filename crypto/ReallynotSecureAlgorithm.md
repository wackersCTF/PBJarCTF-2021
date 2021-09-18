# ReallynotSecureAlgorithm
by 
## Description
Here's the obligatory problem!!!
## Attachments
script.py
```python
from Crypto.Util.number import *
with open('flag.txt','rb') as f:
    flag = f.read().strip()
e=65537
p=getPrime(128)
q=getPrime(128)
n=p*q
m=bytes_to_long(flag)
ct=pow(m,e,n)


print (p)
print (q)
print (e)
print (ct)
```
out.txt
```
194522226411154500868209046072773892801
288543888189520095825105581859098503663
65537
2680665419605434578386620658057993903866911471752759293737529277281335077856
```
## Solution
Really simple.

```python
from Crypto.Util.number import *
def egcd(a, b):
    x,y, u,v = 0,1, 1,0
    while a != 0:
        q, r = b//a, b%a
        m, n = x-u*q, y-v*q
        b,a, x,y, u,v = a,r, u,v, m,n
        gcd = b
    return gcd, x, y

def main():

    p = 194522226411154500868209046072773892801
    q = 288543888189520095825105581859098503663
    e = 65537
    ct = 2680665419605434578386620658057993903866911471752759293737529277281335077856


    # compute n
    n = p * q

    # Compute phi(n)
    phi = (p - 1) * (q - 1)

    # Compute modular inverse of e
    gcd, a, b = egcd(e, phi)
    d = a

    print( "n:  " + str(d) );

    # Decrypt ciphertext
    pt = pow(ct, d, n)
    print( "pt: " + str(pt) )
    print(long_to_bytes(pt))

if __name__ == "__main__":
    main()
```
flag: ```flag{n0t_to0_h4rd_rIt3_19290453}```
