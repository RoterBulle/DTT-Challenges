RED

Approach

Inspected image metadata using exiftool and found an acrostic poem whose initial letters spelled CHECK LSB. 
Checked the pixel array and noticed non-default channel bits clustered uniformly along columns.

Solution

Extracted the least significant bits across channels in column-major order. This revealed a Base64-encoded string: YWNhZGVteXtYM2RfMXNfdGgzX3VsdDFtNHQxX2N1cFNfZjByXzU0ZG4zNTVffQ==. Decoded the string and corrected the byte offsets matching the underlying Bill Blass quote ("Red is the ultimate cure for sadness")
python3 -c "
from PIL import Image
img = Image.open('red.png')
w, h = img.size
bits = [img.getpixel((x, y))[c] & 1 for x in range(w) for c in range(4) for y in range(h)]
data = bytes(sum(b << (7 - j) for j, b in enumerate(bits[i:i+8])) for i in range(0, len(bits) - 7, 8))
print(data)
"

Flag
academy{r3d_1s_th3_ult1m4t3_cur3_f0r_54dn355_}

Takeaway
Check metadata for acrostic clues, and test column-major channel packing when standard row-wise LSB fails
