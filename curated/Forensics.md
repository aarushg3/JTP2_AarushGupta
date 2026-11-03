# Challenge 1 - I Guess Bro
## Description
- Bro said “trust me” and sent an image that won't open. Something seems to be off with the chunks, can you fix it?
- I am given a corrupted png here that i have to fix to get the flag.

## Flag
- nite{nutr3la_d1ed_f0r_th1s}

## Solve
- I first made a copy of the image named temp.png to keep the original safe in case something was to happen while solving. i used the basic commands on the png, file, binwalk, exiftool and xxd. after xxd, i saw that the magic bytes of the image were wrong. then i read the description of the challenge which said something about chunks being off. i had no idea at this point what these chunks are or what they mean. so i started researching. whatever i learned during my research is in the "New Concepts" section. so after my research, i opened the file in ghex. i first fixed the magic bytes from 89 70 6E 67 to 89 50 4E 47. then after learning about chunks and chunk headers, i looked for the IHDR, IEND, IDAT and PLTE headers as i saw they were the "critical chunks". i found that IHDR, IEND, IDAT were written as ihdr, iend, idat so i fixed that however i could not find PLTE. so i looked around more and found that it is optional when the color type is 2 or 6 and is not present when it is 0 or 4. so i found in the IHDR chunk at offset 0x19 that the color type is 2 so i ignored the PLTE chunk and saved the image. i then opened it and the image opened where i got the flag.

## New Concepts
- How do pngs work
- What is lossless compression
- What are huffman codes, filtering, different types of filters ( SUB, UP, PAETH, AVG, NONE), LZSS 
- what is redundancy and how its exploited in lossless compression
- How pngs differ from JPEGs
- what are chunks in pngs
- the inital structure of pngs
- the structure of chunks
- what are critical and ancillary chunks
- use of IHDR ( describes image dimensions, color type, bit depth, etc.) 
- use of PLTE ( contains the color palette of the image)
- use of IDAT ( contains the image data )
- use of IEND ( marks the end of the image)

## Tangents
- no tangents as such, the challenge was pretty straight forward
