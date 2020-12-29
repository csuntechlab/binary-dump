# binary-dump
A web-based version of the "od" (octal dump) unix CLI command

# Description

The binary dump application is a filter that displays input values in three different formats. These format include:
   1. Network Order: A stream of bytes presented in [network order](https://en.wikipedia.org/wiki/Endianness)
   1. Memory Contents: An array of 64-bit structured similiar to the output of the octal dump program
   1. Encodings: A set of mappings from either 16-, 32-, or 64-bit values to varous encodings, e.g., [float16](https://en.wikipedia.org/wiki/Half-precision_floating-point_format)

A view window is used within each of these formats to highlight the set of bytes used as part of the input value. Each indivual byte can be displayed as either binary, octal, hexidecimal, ASCII, or decimal values.

# Input
There are two ways to provide input the application:
  1. a URL that identifies a file that is interpreted as as stream of bytes
  1. a comma (or newline) separates list of values of the following types: byte, char, int32, float32, strings
  
    - alignment: int32, float32, and strings are 4-byte aligned with all others values are byte aligned
    - input formats: C-style input, base#number, scientific notation (d.dddEdd)

# Output
There are three general output displays for this application: network order, memory contents, and encodings. The memory-contents and encoding sections are collapable. 

A *view window* is provided in each section to hightlight the current set of bytes used as the input values. This view window can have a 16-bit, 32-bit, or 64-bit width. The data within the view window can be displayed as either binary, octal, hexidecimal, ASCII, or decimal values.

## Network Order
The input values is interpreted as a stream of bytes. A 64-bit vector is provided that contains the defined *view window*. The view window can be moved forward and backward via the defined word size. The view window can also be shifted by double-clicking on an individual byte. This byte becomes the starting point of the view window. Note, however, this shifting of the window can result in data alignment issues.

## Memory Contents
Memory is displayed as an array of 64-bits, within a table containg 4 visable rows. The corresponding location of the *view window* is depicted within the memory array. The values within this view window may have a different order, to illustrate little endian or big endian byte order. The view window is used as the source data for the Encoding 

## Encodings:
Various encodings are provided for the bytes within the current view window. This view window is re-presented, along with the corresponding binary value. Each of the implemented encodings are provide with the structure of format, the associated output value/s, and a status field. The status field indicates whether or not there is a valid encoding and any other types of warnings, e.g., alignment errors.

The current defined set of encodings envision to be supported include:
  - unary:
  - decimal:
    - decimal: unsigned
    - decimal: two's complement
    - decimal: one's complement
    - BCD 8421 : packed 
  - Character:
    - ASCII
    - UTF-8
  - Floating Point:
    - float8 (contrived)
    - float16 (half)
    - float32 (single)
    - float64 (double)
  - Other:
    - base64
    - RGB (8-bit channel):  top order must be zero (XXXX)
    - RGB (10-bit channel): top tow bits must be XX
 
