# image-steg
Easy, basic image Steganography commands and tools for CTF, DFIR etc.

### # CTF IMAGE STEGANOGRAPHY CHECKLIST

Each example image contains a flag.

**1. File**

Just to be sure what file you are facing with, check its type with type filename.

`file xxx.png `

**2. Strings**

View all strings in the file

We use -n 7 for strings of length 7+, and -t x to view- their position in the file.

Alternatively, you can view strings on this site once an image has been uploaded at https://www.aperisolve.com/

`strings -n 7 -t x filename.png`

**3. Exif**

Check all image metadata. I would recommend Jeffrey's Image Metadata Viewer for in-depth analysis.

Example:

`exif filename `

**4. Binwalk**

We use binwalk to check image's for hidden embedded files.

My preferred syntax, example:

`binwalk -Me filename.png`

-Me is used to recursively extract any files.

**5. pngcheck**

We can use pngcheck to look for optional/correct broken chunks. This is vital if the image appears corrupt.

Example: 

`pngcheck -vtp7f filename.png to view all info.`

v is for verbose, 
t and 7 display tEXt chunks,
p displays contents of some other optional chunks
f forces continuation after major errors are encountered

**6. Explore Colour & Bit Planes**

Images can be hidden inside of the colour/bit planes. Upload your image to this site here. On the image menu page, explore all options in the top panel (i.e. Full Red, Inverse, LSB etc).

Go to "Browse Bit Planes", and browse through all available planes.

If there appears to be some static at the top of any planes, try extracting the data from them in the "Extract Files/Data" menu.

**7. Extract LSB Data**

As mentioned in step 5, there could be some static in bit planes. If so, navigate to the "Extract Files/Data" page, and select the relevant bits.


**8. Check RGB Values**

ASCII Characters/other data can be hidden in the RGB(A) values of an image.

Upload your image here, and preview the RGBA values. Try converting them to text, and see if any flag is found. It might be worth looking at just the R/G/B/A values on their own.

**9. Found a password? (Or not)**

If you've found a password, go to application to check should be steghide. Bear in mind that steghide can be used without a password, too.

You can extract data by running:

`steghide extract -sf filename.png.`

It might also be worth checking some other tools:

    OpenStego
    Stegpy
    Outguess
    jphide

**10. Browse Colour Palette**

If the PNG is in type 3, you should look through the colour palette.

This site has a feature for randomizing the colour palette, which may reveal the flag. You can also browse through each colour in the palette, if the flag is the same colour.

It may also be worth looking at the palette indexes themselves, as a string may be visible from there.

**11. Pixel Value Differencing (PVD/MPVD)**

It would be rare to have a case of PVD where you're not explicitly told that this is the steganographic method, as it's very niche.

However, this is a method where the differences between pixel pairs are measured slightly adjusted in order to hide data.


