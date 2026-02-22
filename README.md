# x96-combiner
A tool for building multi-architecture (x86/x64) shellcode that can execute correctly on both platforms.\
The implementation is inspired by techniques observed in DoublePulsar.
## Usage
```bash
x96-combiner -x86 x86.bin -x64 x64.bin -o x96.bin
```
## Development
```go
package main

import (
    "fmt"

    "github.com/RTS-Framework/x96-combiner"
)

func main() {
    x86 := []byte{
        0x31, 0xC0,                   // xor eax, eax
        0x05, 0x86, 0x00, 0x00, 0x00, // add eax, 0x86
        0xC3,                         // ret
    }
    x64 := []byte{
        0x31, 0xC0,                   // xor eax, eax
        0x48, 0x83, 0xC0, 0x64,       // add rax, 0x64       
        0xC3,                         // ret
    }
    shellcode := combiner.Combine(x86, x64)
    fmt.Println(shellcode)
}
```
