# Setup MASM development environment in Linux

## Install dosemu

Clone git repository from: https://github.com/stsp/dosemu2.git

Following instuctions in INSTALL file:

```
./autogen.sh

./default-configure

make
```

Download Freedos bin file from dosemu.org.

```
sudo make install
```

Test if dosemu works:

```
$> dosemu -t

```

## Install MASM binary

Download zip: http://www2.hawaii.edu/~pager/312/masm%20615%20downloading.htm

Unzip it to local folder:

```
$> mkdir masm
$> unzip masm-615.zip -d masm
$> sudo ln -s masm ~/.dosemu/drives/d/masm-bin
```

## Verification

```
$> dosemu -t
C:\> D:
D:\> cd masm-bin
D:\masm-bin>masm.exe
Microsoft (R) MASM Compatibility Driver Version 6.11
Copyright (C) Microsoft Corp 1993.  All rights reserved.

usage: MASM [option...] source(.asm),[out(.obj)],[list(.lst)],[cref(.crf)][;]
Run "MASM /H" for more info
D:\masm-bin>

```

Done!

## Troubleshooting

### Q: Failed to build from source code from dosemu.org

> A: It's yacc/flex related issue of conflict definition. Using source in github to solve it.
