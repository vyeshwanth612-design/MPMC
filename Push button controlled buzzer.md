## Design and Implementation of a Push-Button-Controlled Buzzer and Speaker Using AT89C51 Microcontroller

## Aim
To interface a buzzer with the 8051 (AT89C51) microcontroller and control the buzzer using a push-button switch.

## Apparatus Required

AT89C51/AT89S52 Microcontroller

Proteus Professional

Keil µVision IDE

BC547 NPN Transistor

330 Ω Resistor

Push Button Switch

Buzzer

0.1 µF Capacitor

Power Supply (+5 V)

## Pin Connections

| Component    | 8051 Pin                         | Description                          |
|--------------|----------------------------------|--------------------------------------|
| Push Button  | P1.4                             | Digital input                        |
| Buzzer Driver| P3.2                             | Digital output to BC547 base through 330 Ω |
| BC547        | Collector → Buzzer, Emitter → GND | Switching transistor               |
| Buzzer       | +5 V and BC547 Collector         | Audible output                       |
| Reset        | RST                              | Reset network                        |

## Theory

The 8051 microcontroller cannot directly drive most buzzers because of current limitations. 
A BC547 transistor is used as a switching device. When Port 3.2 becomes HIGH, the transistor 
turns ON and current flows through the buzzer, producing sound. When Port 3.2 is LOW, the 
transistor turns OFF and the buzzer remains silent.

## Algorithm

1.Start the program.
2.Configure P1.4 as input and P3.2 as output.
3.Read the push-button status continuously.
4.If P1.4 = 1, make P3.2 = 1 to turn ON the buzzer.
5.If P1.4 = 0, make P3.2 = 0 to turn OFF the buzzer.
6.Repeat continuously.

## Procedure

1. Create a new 8051 project in Keil µVision and select the AT89C51/AT89S52 device.
2. Create an ASM source file and enter the given assembly program.
3. Build the project and generate the HEX file.
4. Open the supplied Proteus circuit and double-click the microcontroller.
5. Load the generated HEX file into the Program File field.
6. Set a suitable crystal frequency and run the simulation.
7. Operate the switch connected to P1.4 and observe the buzzer connected through the BC547 transistor.

## 8051 Assembly Language Program

**Program objective:** Read the switch connected to P1.4 and control the buzzer connected to P3.2.

```asm
ORG 0000H

        CLR     P1.4

BACK:   CLR     P3.2

WAIT:   JNB     P1.4, WAIT
        SETB    P3.2
        ACALL   DELAY

WAIT1:  JB      P1.4, WAIT1
        SJMP    BACK

DELAY:
        MOV     R0, #255
HERE1:  MOV     R1, #255
HERE:   DJNZ    R1, HERE
        DJNZ    R0, HERE1
        RET

        END
```

<img width="719" height="720" alt="image" src="https://github.com/user-attachments/assets/3e0fb38d-4005-4734-87c6-9a911e3c9f6e" />


## Program Explanation

| Instruction | Function |
|---|---|
| ORG 0000H | Places the program starting address at memory location 0000H. |
| CLR P1.4 | Initially clears the switch input pin P1.4. |
| CLR P3.2 | Turns OFF the buzzer connected to P3.2. |
| JNB P1.4, WAIT | Waits while P1.4 is LOW. The program continues when the switch input becomes HIGH. |
| SETB P3.2 | Makes P3.2 HIGH and turns ON the buzzer. |
| ACALL DELAY | Calls the delay subroutine. |
| JB P1.4, WAIT1 | Keeps checking the input while P1.4 remains HIGH. |
| SJMP BACK | Returns to the beginning and turns OFF the buzzer after the switch is released. |
| DJNZ R1 / DJNZ R0 | Creates a software delay using two nested loops. |
| RET | Returns from the delay subroutine. |
| END | Marks the end of the assembly program. |

## Output image from proteus
<img width="1600" height="898" alt="WhatsApp Image 2026-11-05 at 10 19 38 AM" src="https://github.com/user-attachments/assets/2d798cda-56ef-45f7-94fd-5649007daf57" />

## Output image from Keil µVision
<img width="1600" height="807" alt="WhatsApp Image 2026-11-05 at 10 16 24 AM" src="https://github.com/user-attachments/assets/9a23c4a0-7ed3-4007-9daf-dcb1e009d8fb" />



## Result
When the push button connected to P1.4 is pressed, the buzzer sounds. When the push button is released, 
the buzzer stops. The Proteus simulation verifies successful interfacing of the buzzer with the 8051 microcontroller.
