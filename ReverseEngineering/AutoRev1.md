Autorev 1

Approach

Connected to the challenge server via netcat, which served hex-encoded ELF binaries requiring answers within a 10-second timeout across 20 rounds. 
Disassembled the binary to locate the comparison logic

Solution
The compiled template moved the secret integer directly into [rbp-0x4] via the opcode sequence \xc7\x45\xfc (mov DWORD PTR [rbp-0x4], imm32). 
Automated parsing the 4-byte immediate value and interacting with the socket using pwntools

import struct
from pwn import remote

io = remote("xebec.cylabacademy.net", 18601)

for _ in range(20):
    io.recvuntil(b"bytes:\n")
    elf = bytes.fromhex(io.recvline().strip().decode())
    idx = elf.find(b"\xc7\x45\xfc")
    secret = struct.unpack("<I", elf[idx + 3 : idx + 7])[0]
    io.recvuntil(b"What's the secret?:")
    io.sendline(str(secret).encode())

print(io.recvall().decode())

Flag


Takeaway
Automate repetitive binary challenges by searching for fixed opcode patterns instead of fully disassembling each binary.
