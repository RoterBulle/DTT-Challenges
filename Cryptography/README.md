EVEN RSA CAN BE BROKEN???

Approach
Evaluated the RSA parameters from encrypt.py and the challenge description. Standard 1024-bit RSA with public exponent e = 65537 cannot be factored directly, but the challenge name suggested that we should take further exploration and manipulation into even modulus N.

Solution
Verified that N is even, making p = 2 a factor. Factored N directly by setting q = N // 2, computed Euler's totient phi(N) = q - 1, derived private exponent d = e^-1 (mod phi), and decrypted the ciphertext.

from pwn import remote
from Crypto.Util.number import long_to_bytes

io = remote("xebec.cylabacademy.net", 32034)
io.recvuntil(b"N: ")
N = int(io.recvline().strip())
io.recvuntil(b"e: ")
e = int(io.recvline().strip())
io.recvuntil(b"cyphertext: ")
c = int(io.recvline().strip())
io.close()

p = 2
q = N // 2
phi = (p - 1) * (q - 1)
d = pow(e, -1, phi)
print(long_to_bytes(pow(c, d, N)).decode())

Flag
academy{tw0_1$_pr!m3cfb893a9}

Takeaway
If an RSA modulus is even, 2 is an immediate factor that breaks the key instantly.

