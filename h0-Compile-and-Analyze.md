### a)

Luodaan C ohjelma
````bash
nano hello_world.c
````
````c
#include <stdio.h>

int main() {
  printf("hello world\n");
}
````
Käytetään gcc luotuun c ohjemlaan.
````bash
gcc hello_world.c
````
Käytetään file komento jotta voidaan analysoida ohjelma.
````bash
file a.out
````
Tulostus
````bash
a.out: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=312e5f6b0ed0249a3950f8049d5a008a0d372893, for GNU/Linux 3.2.0, not stripped
````

### Lähteet:
Uppmax: https://docs.uppmax.uu.se/software/gcc_compile_c/

