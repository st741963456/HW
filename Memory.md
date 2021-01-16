> **Memory**
```
/**
 * The complete address space of the Hack computer's memory,
 * including RAM and memory-mapped I/O. 
 * The chip facilitates read and write operations, as follows:
 *     Read:  out(t) = Memory[address(t)](t)
 *     Write: if load(t-1) then Memory[address(t-1)](t) = in(t-1)
 * In words: the chip always outputs the value stored at the memory 
 * location specified by address. If load==1, the in value is loaded 
 * into the memory location specified by address. This value becomes 
 * available through the out output from the next time step onward.
 * Address space rules:
 * Only the upper 16K+8K+1 words of the Memory chip are used. 
 * Access to address>0x6000 is invalid. Access to any address in 
 * the range 0x4000-0x5FFF results in accessing the screen memory 
 * map. Access to address 0x6000 results in accessing the keyboard 
 * memory map. The behavior in these addresses is described in the 
 * Screen and Keyboard chip specifications given in the book.
 */

CHIP Memory {
    IN in[16], load, address[15];
    OUT out[16];

    PARTS:
    Not(in=address[14],out=x);
    And(a=address[14],b=load,out=Sload);
    And(a=x,b=load,out=Rload);

    RAM16K(in=in,address=address[0..13],load=Rload,out=R);
    Screen(in=in,address=address[0..12],load=Sload,out=S);
    Keyboard(out=Kout);

    Mux16(a=S,b=Kout,sel=address[13],out=outSK);
    Mux16(a=R,b=outSK,sel=address[14],out=out);
}
```

![Mem](https://user-images.githubusercontent.com/36965820/104498575-d0f63e00-5616-11eb-84a3-2e6d9adb7121.jpg)
