> **ALU-nostat**
```
CHIP ALU {
    IN  
        x[16], y[16],  // 16-bit inputs        
        zx, // zero the x input?
        nx, // negate the x input?
        zy, // zero the y input?
        ny, // negate the y input?
        f,  // compute out = x + y (if 1) or x & y (if 0)
        no; // negate the out output?

    OUT 
        out[16], // 16-bit output
        zr, // 1 if (out == 0), 0 otherwise
        ng; // 1 if (out < 0),  0 otherwise

    PARTS:
        
        Mux16(a=x, b=false, sel=zx, out=x1);
        Mux16(a=y, b=false, sel=zy, out=y1);
        Not16(in=x1, out=x1b);
        Not16(in=y1, out=y1b);
        Mux16(a=x1, b=x1b, sel=nx, out=x2);
        Mux16(a=y1, b=y1b, sel=ny, out=y2);
        Add16(a=x2, b=y2, out=p);
        And16(a=x2, b=y2, out=q);
        Mux16(a=q, b=p, sel=f, out=k);
        Not16(in=k, out=kb);
        Mux16(a=k, b=kb, sel=no, out=out);
}
```

> **ALU**
```
    PARTS:
        
        Mux16(a=x, b=false, sel=zx, out=x1);
        Mux16(a=y, b=false, sel=zy, out=y1);
        Not16(in=x1, out=x1b);
        Not16(in=y1, out=y1b);
        Mux16(a=x1, b=x1b, sel=nx, out=x2);
        Mux16(a=y1, b=y1b, sel=ny, out=y2);
        Add16(a=x2, b=y2, out=p);
        And16(a=x2, b=y2, out=q);
        Mux16(a=q, b=p, sel=f, out=k);
        Not16(in=k, out=kb);
        Mux16(a=k, b=kb, sel=no, out=out, out[0..7]=m, out[8..15]=o, out[15]=ng);

        Or8Way(in=m, out=mo);
        Or8Way(in=o, out=oo);
        Or(a=mo, b=oo, out=G);
        Not(in=G, out=zr);
}
```

![ALU](https://user-images.githubusercontent.com/36965820/104126809-ab103580-5399-11eb-85b4-dcaaca79b4fb.jpg)