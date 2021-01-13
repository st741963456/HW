> **PC**
```
/**
 * A 16-bit counter with load and reset control bits.
 * if      (reset[t] == 1) out[t+1] = 0
 * else if (load[t] == 1)  out[t+1] = in[t]
 * else if (inc[t] == 1)   out[t+1] = out[t] + 1  (integer addition)
 * else                    out[t+1] = out[t]
 */

CHIP PC {
    IN in[16],load,inc,reset;
    OUT out[16];

    PARTS:
    Inc16(in=PC, out=IncPC);
    Mux16(a=PC, b=IncPC, sel=inc, out=outx);
    Mux16(a=outx, b=in, sel=load, out=outy);
    Mux16(a=outy, b=false, sel=reset, out=outz);
    Register(in=outz, load=true, out=PC, out=out);
}
```
![PC](https://user-images.githubusercontent.com/36965820/104422093-387ca100-55b7-11eb-9fb9-33b1df31d005.jpg)
