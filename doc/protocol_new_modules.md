# Protocol annax split flap display

## Gereral

Protocol: `RS485`<br>
Baudrate: `19200 8N1`

## Message Structure

`<BREAK> FF <COMMAND> <ADDR> ( < VALUE1> ( <VALUE2> ..) ) `

- `BREAK` Every message needs to start with an break
- `FF`: Start Byte
- `ADDR`: Module address
- `CMD`: Command
- `DATA`: Data to send. If multiple, sendt to following modules

## Commands

Commands are in HEX

| Command   | Write    | Read     | Description   |
|-----------|----------|----------|---------------|
| DISP/RDB  |   `C0`   |   `D0`   | Set/Get Position |
| STAT      |   `C1`   |   `D1`   | |
| RESET/VER |   `C4`   |   `D4`   | Read: Get firmware version |
| ZERO      |   `C5`   |          | Move to zero point |
| STEP      |   `C6`   |          | Move motor a step (1 blade) forward |
| PULSE     |   `C7`   |          | Move motor a pusle forward |
| TEST      |   `C8`   |          | |
| CTRL      |   `C9`   |   `D9`   | |
| NULL/POS  |   `CA`   |   `DA`   | |
| WIN       |   `CB`   |   `DB`   | Used for calibration |
| CALB      |   `CC`   |   `DC`   | Calibrate |
| TYPE      |   `CD`   |   `DD`   | Set/get type |
| ADDR      |   `CE`   |   `DE`   | Set/get address |
| SNBR      |   `CF`   |   `DF`   | Set/get serial number |


### Set Position
`FF C0 <ADDR> <POS>`<br>
pos is position in bytes

#### Example
Address: 29, Position: 20<br>
`FF CO 1D 14 `

### Get position
`FF DO ADDR`<br>
The module answer 1 bit with position as bytes

#### Example
Address: 29 , Module Position: 30<br>
`FF DO 1D`<br>
Response: <br>
`1E`

### Get serial number
`FF DF <ADDR>`<br>
The module answers with 4 bytes containing the serial number

#### Example
Address: 29 , Module Serial number: 43516<br>
`FF DF 1D`<br>
Response: <br>
`01 88 3f 00`