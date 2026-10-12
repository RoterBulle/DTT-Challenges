Transformation

Approach

Analyzed the provided Python compression expression: ''.join([chr((ord(flag[i]) << 8) + ord(flag[i + 1])) for i in range(0, len(flag), 2)]). 
AI Noticed that pairs of 8-bit ASCII characters were packed into single 16-bit characters. Thus decided to pursue that line of approach.

Solution

Reversed the bit shift for each character in enc by extracting the upper byte (>> 8) and lower byte (& 0xFF):
enc = open('enc').read()
flag = ''.join(chr(ord(c) >> 8) + chr(ord(c) & 0xFF) for c in enc)
print(flag)

Flag
academy{16_bits_inst34d_of_8_790ba37e}   

Takeaway
Reconstruct packed 16-bit characters by splitting high bytes with right shifts and low bytes with bitmasks.   
