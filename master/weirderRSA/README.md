# PicoCTF_2017: weirderRSA

**Category:** Master
**Points:** 175
**Description:**

>Another message encrypted with RSA. It looks like some parameters are missing. Can you still decrypt it? [Message](clue.txt)

**Hint:**

>Is there some way to create a multiple of p given the values you have?
Fermat's Little Theorem may be helpful

## Write-up
Fermat's Little Theorem is an interesting thing that took me awhile to understand, being new to cryptography but essentially what we have to do to break this involves just playing with `dp` to get `p`
    
    r = 123456
    p = gmpy2.gcd(n, pow(r, (e*dp), n) - r)

With `p` found, we can just divide `n` with `p` to get `q`.

    q = gmpy2.div(n, p)

With `q` found, we can calculate `d` to be the inverse of `(p-1)(q-1)`

    phi = (p-1) * (q-1)
    d = gmpy2.invert(e, phi)

With `d` found, the challenge is [solved](solve.py).

Therefore, the flag is `flag{wow_leaking_dp_breaks_rsa?_64151418169}`.