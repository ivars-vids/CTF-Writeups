# Binomial Ways

We are given the following code:
```python
from secret import flag
val = []
flag_length = len(flag)
print(flag_length)

def factorial(n):
    f = 1
    for i in range(2, n+1):
        f *= i
    return f

def series(A, X, n):
    nFact = factorial(n)
    for i in range(0, n + 1):
        niFact = factorial(n - i)
        iFact = factorial(i)
        aPow = pow(A, n - i)
        xPow = pow(X, i)
        val.append(int((nFact * aPow * xPow) / (niFact * iFact)))

A = 1; X = 1; n = 30
series(A, X, n)
ct = []
for i in range(len(flag)):
    ct.append(chr(ord(flag[i])+val[i]%26))
print(''.join(ct))
```
`series`  function all the time generates the same sequence of numbers. For each flag char position it has different number. It acts like Stream crypter.

And the output file:
```
31
27F;VPbAs>clu}={9ln=_o1{0n5tp~
```

It's pretty obvious how to decrypt the message, by simply replacing `ct.append(chr(ord(flag[i])+val[i]%26))` to `ct.append(chr(ord(flag[i])-val[i]%26))`.
After first decryption we get:
```
30
1337UPUAf>Vlh{(o$ja=Ro${#n4p]z
```
we can crealy see that the encrypter flag was shorter by one char, and the result did no mached flag pattern `1337UP{}`. So we need to add one extra char in correct place. we can see that `1337UP` decrypter correctly.

We need to modify encrypted flag from `27F;VPbAs>clu}={9ln=_o1{0n5tp~` to `27F;VP@bAs>clu}={9ln=_o1{0n5tp~`, I added `@` just after `1337UP`.

After second decryption we get:
```
31
1337UP3b4s1c_sh1f7_n0_b1n0m1al}
```
Almost valid flag, at this pint we can simply assume that `3` is `{` and patch the decrypted flag manually.

The final flag `1337UP{b4s1c_sh1f7_n0_b1n0m1al}`
