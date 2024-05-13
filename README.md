# CHIP-8

## Opcodes

> ONLY ORIGINAL CHIP-8 INSTRUCTIONS

|Opcode|Mnemonic|Description|
|--|--|--|
|001N|EXIT `N`|From Peter Miller's chip8run. Exit emulator with a return value of `N`.|
|00E0|CLS|Clears the display. Sets all pixels to `off`.|
|00EE|RET|Return from subroutine. Set the `PC` to the address at the top of the stack and subtract `1` from the `SP`.|
|00FA|COMPAT|Non-standard. Toggles changing of the `I` register by `save (FX55)` and `restore (FX65)` opcodes.|
|0NNN|CALL `NNN`|Call machine language subroutine at address `NNN`.|
|1NNN|JMP `NNN`|Set `PC` to `NNN`.|
|2NNN|CALL `NNN`|Call subroutine a `NNN`. Increment the `SP` and put the current `PC` value on the top of the stack. Then set the `PC` to `NNN`. Generally there is a limit of 16 successive calls.|
|3XNN|SE `VX`, `NN`|Skip the next instruction if register `VX` is equal to `NN`.|
|4XNN|SNE `VX`, `NN`|Skip the next instruction if register `VX` is **not** equal to `NN`.|
|5XY0|SE `VX`, `VY`|Skip the next instruction if register `VX` equals `VY`.|
|6XNN|LD `VX`, `NN`|Load immediate value `NN` into register `VX`.|
|7XNN|ADD `VX`, `NN`|Add immediate value `NN` to register VX. Does **not** effect `VF`.|
|8XY0|LD `VX`, `VY`|Copy the value in register `VY` into `VX`|
|8XY1|OR `VX`, `VY`|Set `VX` equal to the bitwise `or` of the values in `VX` and `VY`.|
|8XY2|AND `VX`, `VY`|Set `VX` equal to the bitwise `and` of the values in `VX` and `VY`.|
|8XY3|XOR `VX`, `VY`|Set `VX` equal to the bitwise `xor` of the values in `VX` and `VY`. **Note:** This instruction was originally undocumented but functional due to how the 8XXX instructions were implemented on teh COSMAC VIP.|
|8XY4|ADD `VX`, `VY`|Set `VX` equal to `VX` plus `VY`. In the case of an overflow `VF` is set to `1`. Otherwise `0`.|
|8XY5|SUB `VX`, `VY`|Set `VX` equal to `VX` minus `VY`. In the case of an underflow `VF` is set `0`. Otherwise `1`. (`VF = VX > VY`)|
|8XY6|SHR `VX`, `VY`|Set `VX` equal to `VX` bitshifted right `1`. `VF` is set to the least significant bit of `VX` prior to the shift. Originally this opcode meant set `VX` equal to `VY` bitshifted right `1` but emulators and software seem to ignore `VY` now. **Note:** This instruction was originally undocumented but functional due to how the 8XXX instructions were implemented on teh COSMAC VIP.|
|8XY7|SUBN `VX`, `VY`|Set `VX` equal to `VY` minus `VX`. `VF` is set to `1` if `VY` > `VX`. Otherwise `0`. **Note:** This instruction was originally undocumented but functional due to how the 8XXX instructions were implemented on teh COSMAC VIP.|
|8XYE|SHL `VX`, `VY`|Set `VX` equal to `VX` bitshifted left `1`. `VF` is set to the most significant bit of `VX` prior to the shift. Originally this opcode meant set `VX` equal to `VY` bitshifted left `1` but emulators and software seem to ignore `VY` now. **Note:** This instruction was originally undocumented but functional due to how the 8XXX instructions were implemented on teh COSMAC VIP.|
|9XY0|SNE `VX`, `VY`|Skip the next instruction if `VX` does **not** equal `VY`.|
|ANNN|LD `I`, `NNN`|Set `I` equal to `NNN`.|
|BNNN|JMP `V0`, `NNN`|Set the `PC` to `NNN` plus the value in `V0`.|
|CXNN|RND `VX`, `NN`|Set `VX` equal to a random number ranging from `0` to `255` which is logically `and`ed with `NN`.|
|DXYN|DRW `VX`, `VY`, `N`|Display `N`-byte sprite starting at memory location `I` at `(VX, VY)`. Each set bit of `xor`ed with what's already drawn. `VF` is set to `1` if a collision occurs. `0` otherwise.|
|EX9E|SKP `VX`|Skip the following instruction if the key represented by the value in `VX` is pressed.|
|EXA1|SKNP `VX`|Skip the following instruction if the key represented by the value in `VX` is **not** pressed.|
|FX07|LD `VX`, `DT`|Set `VX` equal to the `delay timer`.|
|FX0A|LD `VX`, KEY|Wait for a key press and store the value of the key into `VX`.|
|FX15|LD `DT`, `VX`|Set the delay timer `DT` to `VX`.|
|FX18|LD `ST`, `VX`|Set the sound timer `ST` to `VX`.|
|FX1E|ADD `I`, `VX`|Add `VX` to `I`. `VF` is set to `1` if `I > 0x0FFF`. Otherwise set to `0`.|
|FX29|LD `I`, `FONT(VX)`|Set `I` to the address of the CHIP-8 8x5 font sprite representing the value in `VX`.|
|FX33|BCD `VX`|Convert that word to BCD and store the 3 digits at memory location `I` through `I+2`. `I` does not change.|
|FX55|LD `[I]`, `VX`|Store registers `V0` through `VX` in memory starting at location `I`. `I` does not change.|
|FX65|LD `VX`, `[I]`|Copy values from memory location `I` through `I + X` into registers `V0` through `VX`. `I` does not change.|

