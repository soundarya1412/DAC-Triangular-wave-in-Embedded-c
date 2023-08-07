# DAC-Triangular-wave-in-Embedded-c
TRIANGULAR WAVE:
#include <LPC17xx.H>
#include "GLCD.H"
#define __FI 1 
void delay(void) 
{
 unsigned char i;
 for(i=0;i<100;i++);
}
main()
{ 
unsigned int i,j;
 LPC_SC->PCONP |= (1 << 15); 
LPC_GPIO0->FIODIR |= 0x007F8000; 
 LPC_GPIO1->FIODIR |= 0x07F80000;
#ifdef __USE_LCD
 GLCD_Init(); 
 GLCD_Clear(White); 
 GLCD_SetBackColor(Blue);
 GLCD_SetTextColor(White);
 GLCD_DisplayString(0, 0, __FI, " ECE ");
 GLCD_DisplayString(1, 0, __FI, " KRCE ");
 GLCD_DisplayString(2, 0, __FI, " EMBEDDED LAB");
59
 GLCD_SetBackColor(White);
 GLCD_SetTextColor(Blue);
 GLCD_DisplayString(5, 0, __FI, " Dual DAC ");
 GLCD_DisplayString(6, 0, __FI, " Triangular Wave ");
#endif
while(1)
 {
for(i=0; i<0x0FF; i++)
 {
LPC_GPIO0->FIOPIN = (LPC_GPIO0->FIOPIN & 0xFF807FFF) | i << 15; 
LPC_GPIO1->FIOPIN = (LPC_GPIO1->FIOPIN & 0xF807FFFF) | i << 19; 
delay();
 }
 
for(j=0xFF; j>0; j--)
 {
LPC_GPIO0->FIOPIN =(LPC_GPIO0->FIOPIN & 0xFF807FFF) | j << 15; 
LPC_GPIO1->FIOPIN = (LPC_GPIO1->FIOPIN & 0xF807FFFF) | j << 19; 
delay();
 }
}
}
