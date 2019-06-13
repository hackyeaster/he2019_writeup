# hacky easter 2019

## 01 - Twisted

**Solution:**

Modify the provided png using gimp (or some other tool) and use filter like "whirl and pinch" (category distorts) to make the qr code readable.

## 02 - Just Watch

**Solution:**

decode the pictures from provided gif using sign language:

flag: ```givemeasign```


## 03 - Sloppy Encryption

**Solution:**

You have to reverse engineer the ruby script to write a decrypt script:

```python
#!/usr/bin/env python3

import base64
import itertools
import codecs

b = 'K7sAYzGlYx0kZyXIIPrXxK22DkU4Q+rTGfUk9i9vA60C/ZcQOSWNfJLTu4RpIBy/27yK5CBW+UrBhm0='

c = base64.b64decode(b)
x = int.from_bytes(c, byteorder='big')
t = int("5" * 101)
h = hex(int(x // t))[2:]
plaintext = codecs.decode(h, "hex")
print(plaintext)
```

flag: ```n00b_style_crypto```

## 04 - Disco 2

**Solution:**

the qr code is hidden inside the disco ball.

use dev console in chrome/firefox:
```javascript
renderer.autoClear = true;
renderer.setClearColor(0xffffff);

sphereMaterial = new THREE.MeshLambertMaterial({
    color : 0x000000})

for (var i = 0; i < mirrors.length; i++) {
    var m = mirrors[i];
    if ( m[2] > -65 && m[2] < 65 ) {
    mirrorTile = new THREE.Mesh(tileGeom, sphereMaterial);
    mirrorTile.position.set(m[0]+500, m[1]+500, m[2]+500);
    scene.add(mirrorTile);
}
}
```

rotate the picture to get a clear view to the qr code and scan it.

flag: ```he19-r5pN-YIRp-2cyh-GWh8```

## 05 - Call for Papers
Please read and review my CFP document, for the upcoming IAPLI Symposium.
I didn't write it myself, but used some artificial intelligence.
What do you think about it?

**Solution:**

Provided is a docx file. Under properties->Creator you find SCIpher as a hint.
SCIpher is a program that can hide text messages within seemingly innocuous scientific conference advertisements.
Paste the text from the docx to an online decoder:
htt ps://pdos.csail.mit.edu/archive/scigen/scipher.html

flag: ```https://hackyeaster.hacking-lab.com/hackyeaster/images/eggs/5e171aa074f390965a12fdc240.png```

## 06 - Dots

**Solution:**

Decode grille ciphertext
https://merricx.github.io/enigmator/cipher/grille.html
you have to fill the right low square with 2 missing dots.
to decode the ciphertext rotate 90 degress to left (the tool from merricx rotates to right).

```
HELLOBUCK
CHOCOLATE
RDISWHITE
THEPASSWO
```

password: ```WHITECHOCOLATE```

## 07 - Shell we Argument

**Solution:**

Provided is a shell script eggi.sh
I manually debugged the script output by adding "set -x" inside the script. Run the script and provide the requested input the unveal the flag. There must be an easier way, but this will also work.

flag: ```https://hackyeaster.hacking-lab.com/hackyeaster/images/eggs/a61ef3e975acb7d88a127ecd6e156242c74af38c.png```


## 09 - rorriM rorriM

**Solution:**

Provided is a file called evichra.piz. By reversing the order you get archive.zip. So it must be an archive, but with reversed bits.
Use the python script to reverse the file.

```python
f = open('evichra.piz', "rb")
s = f.read()
f.close()
f = open('archive.zip', "wb")
f.write(s[::-1])
f.close()
```

```bash
unzip archive.zip
#extracted file 90gge.gnp
hexdump -C 90gge.gnp # it's a png file but the magic number in the header is not correct. set it to "89 50 4E 47 0D 0A 1A 0A" using hexedit.
mv 90gge.png egg09.png
hexedit egg09.png # modify and save ctrl x + y
```

to get the flag you have to modify the png using horizontal flip and invert colors (use gimp or some other tool)

## 13 - Symphony in HEX

**Solution:**

The hint tells us to count the quavers as numbers and read the semibreves as character:
4841434B5F4D455F414D4144455553
using hex decoder you get the flag:

password: ```HACK_ME_AMADEUS```

## 15 - Seen in Steem

**Solution:**
In Steem blockchain it is possible to place notes in the memo field of transactions.
Found this nice steem transfer viewer tool:
https://steemyy.com/transfer-viewer/
As accountid use "darkstar-42" (I've found the challenge author in steemit) and populate the field "memo contains" with "hacky easter 2019".
The result is a transaction from 2018-04-01T14:39:36 with flag

password: ```nomoneynobunny```


## 18 - Egg Storage

**Solution:**
The egg storage is using a WebAssembly (wasm) technology.
Find the wasm code using Firefox/Chrome debug and reverse engineer the code.
There are 2 interesting function (validate_range, validate_password).
validate_range checks if the password character is an character range of 12 possible characters (48 - "0", 49 - "1", 51 - ", ...).
validate_password verifies the value of the variables $var0 to $var23 using several arithmetic functions. reverse the functions to get the correct password:

passowrd: ```Th3P4r4d0X0fcH01c3154L13```
