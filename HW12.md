> **Computer**
```
/**
 * The HACK computer, including CPU, ROM and RAM.
 * When reset is 0, the program stored in the computer's ROM executes.
 * When reset is 1, the execution of the program restarts. 
 * Thus, to start a program's execution, reset must be pushed "up" (1)
 * and "down" (0). From this point onward the user is at the mercy of 
 * the software. In particular, depending on the program's code, the 
 * screen may show some output and the user may be able to interact 
 * with the computer via the keyboard.
 */

CHIP Computer {

    IN reset;

    PARTS:
    ROM32K(address=pc,out=instruction);
    CPU(inM=inM,instruction=instruction,reset=reset,writeM=writeM,outM=outM,addressM=addressM,pc=pc);
    Memory(in=outM,address=addressM,load=writeM,out=inM);
}
```

![Computer](https://user-images.githubusercontent.com/36965820/104503281-cee2ae00-561b-11eb-9c38-fc5fbf29658d.jpg)
