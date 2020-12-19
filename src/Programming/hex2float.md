# [Half-Precision Floating Point](https://en.wikipedia.org/wiki/Half-precision_floating-point_format)
## IEEE 754 half-precision binary floating-point format: binary16 
* Sign bit: 1 bit
* Exponent Width: 5 bits
* Significant Precision: 11 bits (10 explicitly stored)

![Half-Precision Format](https://upload.wikimedia.org/wikipedia/commons/2/21/IEEE_754r_Half_Floating_Point_Format.svg)

The format is assumed to have an implicit lead bit with value 1 until the exponent field is stores with all zeros.

## Exponent Encoding
The half-precision binary floating-point exponent is encoding using an offset-binary representation with the zero offset being 15.

### Offset-Binary
Offset binary is a coding scheme where all-zero corresponds to the minimal negative value and all-one to the maximal positive value. There is no standard for offset binary, but most often the offset $K$ for an n-bit binary word is $K = 2^{n-1}.$ 
