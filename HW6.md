> **RAM-8**
```
/**
 * Memory of 8 registers, each 16 bit-wide. Out holds the value
 * stored at the memory location specified by address. If load==1, then 
 * the in value is loaded into the memory location specified by address 
 * (the loaded value will be emitted to out from the next time step onward).
 */

CHIP RAM8 {
    IN in[16], load, address[3];
    OUT out[16];

    PARTS:
    DMux8Way(in= load, sel= address, a=x0, b=x1, c=x2, d=x3, e=x4, f=x5, g=x6, h=x7);
    Register(in=in, load=x0, out=y0);
    Register(in=in, load=x1, out=y1);
    Register(in=in, load=x2, out=y2);
    Register(in=in, load=x3, out=y3);
    Register(in=in, load=x4, out=y4);
    Register(in=in, load=x5, out=y5);
    Register(in=in, load=x6, out=y6);
    Register(in=in, load=x7, out=y7);
    Mux8Way16(a=y0, b=y1, c=y2, d=y3, e=y4, f=y5, g=y6, h=y7, sel= address, out=out);
}
```
![RAM8](https://user-images.githubusercontent.com/36965820/104420022-3d8c2100-55b4-11eb-9d4a-ebdcd6fb90ab.jpg)

> **RAM-64**
```
/**
 * Memory of 64 registers, each 16 bit-wide. Out holds the value
 * stored at the memory location specified by address. If load==1, then 
 * the in value is loaded into the memory location specified by address 
 * (the loaded value will be emitted to out from the next time step onward).
 */

CHIP RAM64 {
    IN in[16], load, address[6];
    OUT out[16];

    PARTS:
    DMux8Way(in= load, sel= address[3..5], a=x0, b=x1, c=x2, d=x3, e=x4, f=x5, g=x6, h=x7);
    RAM8(in=in, load=x0, address=address[0..2], out=y0);
    RAM8(in=in, load=x1, address=address[0..2], out=y1);
    RAM8(in=in, load=x2, address=address[0..2], out=y2);
    RAM8(in=in, load=x3, address=address[0..2], out=y3);
    RAM8(in=in, load=x4, address=address[0..2], out=y4);
    RAM8(in=in, load=x5, address=address[0..2], out=y5);
    RAM8(in=in, load=x6, address=address[0..2], out=y6);
    RAM8(in=in, load=x7, address=address[0..2], out=y7);
    Mux8Way16(a=y0, b=y1, c=y2, d=y3, e=y4, f=y5, g=y6, h=y7, sel= address[3..5], out=out);
}
```
![RAM64](https://user-images.githubusercontent.com/36965820/104420060-4977e300-55b4-11eb-9c5b-589ff5461b59.jpg)

> **RAM-512**
```
/**
 * Memory of 512 registers, each 16 bit-wide. Out holds the value
 * stored at the memory location specified by address. If load==1, then 
 * the in value is loaded into the memory location specified by address 
 * (the loaded value will be emitted to out from the next time step onward).
 */

CHIP RAM512 {
    IN in[16], load, address[9];
    OUT out[16];

    PARTS:
    DMux8Way(in= load, sel= address[6..8], a=x0, b=x1, c=x2, d=x3, e=x4, f=x5, g=x6, h=x7);
    RAM64(in=in, load=x0, address=address[0..5], out=y0);
    RAM64(in=in, load=x1, address=address[0..5], out=y1);
    RAM64(in=in, load=x2, address=address[0..5], out=y2);
    RAM64(in=in, load=x3, address=address[0..5], out=y3);
    RAM64(in=in, load=x4, address=address[0..5], out=y4);
    RAM64(in=in, load=x5, address=address[0..5], out=y5);
    RAM64(in=in, load=x6, address=address[0..5], out=y6);
    RAM64(in=in, load=x7, address=address[0..5], out=y7);
    Mux8Way16(a=y0, b=y1, c=y2, d=y3, e=y4, f=y5, g=y6, h=y7, sel= address[6..8], out=out);
```
![RAM512](https://user-images.githubusercontent.com/36965820/104420086-509ef100-55b4-11eb-8acd-dc998608e829.jpg)

> **RAM-4K**
```
/**
 * Memory of 4K registers, each 16 bit-wide. Out holds the value
 * stored at the memory location specified by address. If load==1, then 
 * the in value is loaded into the memory location specified by address 
 * (the loaded value will be emitted to out from the next time step onward).
 */

CHIP RAM4K {
    IN in[16], load, address[12];
    OUT out[16];

    PARTS:
    DMux8Way(in= load, sel= address[9..11], a=x0, b=x1, c=x2, d=x3, e=x4, f=x5, g=x6, h=x7);
    RAM512(in=in, load=x0, address=address[0..8], out=y0);
    RAM512(in=in, load=x1, address=address[0..8], out=y1);
    RAM512(in=in, load=x2, address=address[0..8], out=y2);
    RAM512(in=in, load=x3, address=address[0..8], out=y3);
    RAM512(in=in, load=x4, address=address[0..8], out=y4);
    RAM512(in=in, load=x5, address=address[0..8], out=y5);
    RAM512(in=in, load=x6, address=address[0..8], out=y6);
    RAM512(in=in, load=x7, address=address[0..8], out=y7);
    Mux8Way16(a=y0, b=y1, c=y2, d=y3, e=y4, f=y5, g=y6, h=y7, sel= address[9..11], out=out);
}
```
![4K](https://user-images.githubusercontent.com/36965820/104420111-598fc280-55b4-11eb-8c35-ab0764de099d.jpg)

> **RAM-16K**
```
/**
 * Memory of 16K registers, each 16 bit-wide. Out holds the value
 * stored at the memory location specified by address. If load==1, then 
 * the in value is loaded into the memory location specified by address 
 * (the loaded value will be emitted to out from the next time step onward).
 */

CHIP RAM16K {
    IN in[16], load, address[14];
    OUT out[16];

    PARTS:
    DMux4Way(in= load, sel= address[12..13], a=x0, b=x1, c=x2, d=x3);
    RAM4K(in=in, load=x0, address=address[0..11], out=y0);
    RAM4K(in=in, load=x1, address=address[0..11], out=y1);
    RAM4K(in=in, load=x2, address=address[0..11], out=y2);
    RAM4K(in=in, load=x3, address=address[0..11], out=y3);
    Mux4Way16(a=y0, b=y1, c=y2, d=y3, sel= address[12..13], out=out);
}
```
![16K](https://user-images.githubusercontent.com/36965820/104420129-601e3a00-55b4-11eb-9c43-f27d81531baa.jpg)
