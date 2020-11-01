ColorJizz is a PHP library for manipulating and converting colors.

---

## Supported formats

```c#
new RGB(r, g, b);
new CMY(c, m, y);
new CMYK(c, m, y, k);
new Hex(0x000000);
new HSV(h, s, v);
new CIELab(l, a, b);
new CIELCh(l, c, h);
new XYZ(x, y, z);
new Yxy(Y, x, y);
```

## Conversion functions

```c#
.toRGB().ToString();
.toCMY().ToString();
.toCMYK().ToString();
.toHex().ToString();
.toHSV().ToString();
.toCIELab().ToString();
.toCIELCh().ToString();
.toXYZ().ToString();
.toYxy().ToString();
```