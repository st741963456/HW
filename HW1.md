> **NOT:**

```
/**
 * Not gate:
 * out = not in
 */

CHIP Not {
    IN in;
    OUT out;

    PARTS:
    Nand(a=in, b=in, out=out);
}
```
```
|  in   |  out  |
|   0   |   1   |
|   1   |   0   |
```
![NOT](https://user-images.githubusercontent.com/36965820/94030730-bc383500-fdf0-11ea-888d-fd08db0050cf.jpg)

> **AND:**

```
/**
 * And gate: 
 * out = 1 if (a == 1 and b == 1)
 *       0 otherwise
 */

CHIP And {
    IN a, b;
    OUT out;

    PARTS:
    Nand(a=a, b=b, out=ANandB);
    Not(in=ANandB, out=out);
}
```
```
|   a   |   b   |  out  |
|   0   |   0   |   0   |
|   0   |   1   |   0   |
|   1   |   0   |   0   |
|   1   |   1   |   1   |
```
![AND](https://user-images.githubusercontent.com/36965820/94030900-e7228900-fdf0-11ea-9a0e-c5c4aa0aa1f3.jpg)

> **OR:**

```
 /**
 * Or gate:
 * out = 1 if (a == 1 or b == 1)
 *       0 otherwise
 */

CHIP Or {
    IN a, b;
    OUT out;

    PARTS:
    Not(in=a ,out=na);
    Not(in=b, out=nb);
    Nand(a=na, b=nb, out=out);
}
```
```
|   a   |   b   |  out  |
|   0   |   0   |   0   |
|   0   |   1   |   1   |
|   1   |   0   |   1   |
|   1   |   1   |   1   |
```
![OR](https://user-images.githubusercontent.com/36965820/94031006-015c6700-fdf1-11ea-97b9-f76a1c7943bd.jpg)

> **XOR:**

```
/**
 * Exclusive-or gate:
 * out = not (a == b)
 */

CHIP Xor {
    IN a, b;
    OUT out;

    PARTS:
    Not(in=a, out=Na);
    Not(in=b, out=Nb);
    And(a=a, b=Nb, out=Xa);
    And(a=Na, b=b, out=Xb);
    Or(a=Xa, b=Xb, out=out);
}
```
```
|   a   |   b   |  out  |
|   0   |   0   |   0   |
|   0   |   1   |   1   |
|   1   |   0   |   1   |
|   1   |   1   |   0   |
```
![XOR](https://user-images.githubusercontent.com/36965820/94031088-133e0a00-fdf1-11ea-8abf-45b93361c0ee.jpg)

> **MUX:**

```
/** 
 * Multiplexor:
 * out = a if sel == 0
 *       b otherwise
 */

CHIP Mux {
    IN a, b, sel;
    OUT out;

    PARTS:
    Not(in=sel, out= nsel);
    And(a=a, b=nsel, out=ax);
    And(a=sel, b=b, out=bx);
    Or(a=ax, b=bx, out=out);
}
```
```
|   a   |   b   |  sel  |  out  |
|   0   |   0   |   0   |   0   |
|   0   |   0   |   1   |   0   |
|   0   |   1   |   0   |   0   |
|   0   |   1   |   1   |   1   |
|   1   |   0   |   0   |   1   |
|   1   |   0   |   1   |   0   |
|   1   |   1   |   0   |   1   |
|   1   |   1   |   1   |   1   |
```
![MUX](https://user-images.githubusercontent.com/36965820/94031171-281a9d80-fdf1-11ea-9327-f0a7bd815a1b.jpg)

> **DMUX:**

```
/**
 * Demultiplexor:
 * {a, b} = {in, 0} if sel == 0
 *          {0, in} if sel == 1
 */

CHIP DMux {
    IN in, sel;
    OUT a, b;

    PARTS:
    Not(in=sel, out=Nsel);
    And(a=in, b=Nsel, out=a);
    And(a=sel, b=in, out=b);
}
```
```
|  in   |  sel  |   a   |   b   |
|   0   |   0   |   0   |   0   |
|   0   |   1   |   0   |   0   |
|   1   |   0   |   1   |   0   |
|   1   |   1   |   0   |   1   |

```
![DMUX](https://user-images.githubusercontent.com/36965820/94031225-39fc4080-fdf1-11ea-9659-76b1be27badf.jpg)
