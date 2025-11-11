# INTERFACING-OF-STEPPER-MOTOR-WITH-ARM-PROCESSOR.

# AIM:
To write an embedded c program to interface STEPPER MOTOR with ARM processor
LPC1768.

# COMPONENTS REQUIRED:
HARDWARE:
ARM LPC 1768
STEPPER MOTOR.
SOFTWARE:
KEIL MICRO VISION 4.0 IDE

# PROCEDURE:

⮚	Open the Keil software and select the New uvision project from Project Menu as shown below.
⮚	Browse to your project folder and provide the project name and click on save.

⮚	Once the project is saved a new pop up “Select Device for Target” opens, Select the controller (NXP: LPC1768) from NXP (founded by philips) and click on OK.
⮚	Select the controller (NXP: LPC1768) and click on OK.

⮚	As LPC1768 needs the startup code, click on Yes option to include the LPC17xx Startup file.
⮚	Create a new file by file → new to write the program.

⮚	Type the code.

⮚	After typing the code save the file as main.c eg. (abc.c).

⮚	Right click target and Add the suitable files to source group1 and header.
 
⮚	Add the main.c along with system_LPC17xx.c.

⮚	Build the project and fix the compiler errors/warnings if any.

⮚	Code is compiled with no errors. The .bin file is still not generated.
⮚	Right Click on Target Options to select the option for generating .bin file.

⮚	Set IROM1 start address as 0x2000. Bootloader will be stored from 0x0000-0x2000 so application should start from 0x2000

⮚	Write	the	command	to	generate	the .bin file	from
.axf file 
Command: fromelf --bin projectname.axf --output filename.bin
⮚	in c/c++ → include paths → desktop (00-libfiles).

⮚	.Bin file is generated after a rebuild.

⮚	Check the project folder for the generated .Bin file.

# ADD FILES:
Target1:
Source group1:
Startuplpc17xx.s, main.c (t), delay.c (t), systemlpc17xx.c (t), gpio.c (t)
Header:
Delay.h, stdutils.h, gpioi.h

# PIN DIAGRAM:

<img width="731" height="473" alt="image" src="https://github.com/user-attachments/assets/5421ccf6-fa3f-43ee-9c80-8300ec5f95fb" />

# CIRCUIT DIAGRAM:

<img width="763" height="357" alt="image" src="https://github.com/user-attachments/assets/2fdb851f-1148-48f4-aed7-9391149248a2" />

# PROGRAM:
```C
#include<lpc17xx.h>
#include "gpio.h"
#define pin1 20
#define pin2 21
#define pin3 22
#define pin4 23
#define control LPC_GPIO1-
>FIOPIN
void cmotor1()
{
control |=(1<<pin1);
control |=(1<<pin2);
control &=~(1<<pin3);
control &=~(1<<pin4);
}
void cmotor2()
{
control &=~(1<<pin1);
control |=(1<<pin2);
control |=(1<<pin3);
control &=~(1<<pin4);
}
void cmotor3()
{
control &=~(1<<pin1);
control &=~(1<<pin2);
control |=(1<<pin3);
control |=(1<<pin4);
29
}
void cmotor4()
{
control |=(1<<pin1);
control &=~(1<<pin2);
control &=~(1<<pin3);
control |=(1<<pin4);
}
void delay_ms(unsigned int ms)
{
unsigned int i,j;
for(i=0;i<ms;i++)
for(j=0;j<20000;j++);
}
int main()
{
SystemInit();
//Clock and PLL configuration
LPC_PINCON->PINSEL3 =
0x000000;
LPC_GPIO1->FIODIR
=(1<<pin1)|(1<<pin2)|(1<<pin3)
| (1<<pin4);
while(1)
{
cmotor1();
delay_ms(50);
cmotor2();
delay_ms(50);
cmotor3();
delay_ms(50);
cmotor4();
delay_ms(50);
}
}
```
# OUTPUT:

![WhatsApp Image 2025-11-11 at 14 17 54_e81fb673](https://github.com/user-attachments/assets/da1d0644-d728-4b92-b6b5-2b92e5213c82)

https://github.com/user-attachments/assets/9ea42892-bc57-487b-ad5f-31ea22fbd337

# RESULT: 
Thus interfacing STEPPER MOTOR with ARM processor LPC1768 is verified.
