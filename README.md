# yedidarebecachavez
codigo
CODIGO ADC DE 8 BITS /*

File: main.c
Author: HP
Created on 23 de octubre de 2019, 20:42 */
#include <xc.h> #include <stdio.h> #include "config.h" unsigned int counter=0;

// PIC16F887 Configuration Bit Settings

// 'C' source line config statements

// CONFIG1 #pragma config FOSC = INTRC_NOCLKOUT// Oscillator Selection bits (INTOSCIO oscillator: I/O function on RA6/OSC2/CLKOUT pin, I/O function on RA7/OSC1/CLKIN) #pragma config WDTE = OFF // Watchdog Timer Enable bit (WDT disabled and can be enabled by SWDTEN bit of the WDTCON register) #pragma config PWRTE = OFF // Power-up Timer Enable bit (PWRT disabled) #pragma config MCLRE = OFF // RE3/MCLR pin function select bit (RE3/MCLR pin function is digital input, MCLR internally tied to VDD) #pragma config CP = OFF // Code Protection bit (Program memory code protection is disabled) #pragma config CPD = OFF // Data Code Protection bit (Data memory code protection is disabled) #pragma config BOREN = ON // Brown Out Reset Selection bits (BOR enabled) #pragma config IESO = ON // Internal External Switchover bit (Internal/External Switchover mode is enabled) #pragma config FCMEN = ON // Fail-Safe Clock Monitor Enabled bit (Fail-Safe Clock Monitor is enabled) #pragma config LVP = ON // Low Voltage Programming Enable bit (RB3/PGM pin has PGM function, low voltage programming enabled)

// CONFIG2 #pragma config BOR4V = BOR40V // Brown-out Reset Selection bit (Brown-out Reset set to 4.0V) #pragma config WRT = OFF // Flash Program Memory Self Write Enable bits (Write protection off)

// #pragma config statements should precede project file includes. // Use project enums instead of #define for ON and OFF.

#INCLUDE <16f887.h> #device adc=10 #USE DELAY(CLOCK=4000000) #FUSES XT,NOPROTECT,NOWDT,NOBROWNOUT,NOPUT,NOLVP #INCLUDE <LCD.C>

#BYTE PORTA= 5 #BYTE PORTD= 8

long bits;
float tem;

void main() { set_tris_a(0b00000001);
set_tris_d(0);
setup_adc_ports(all_analog);
setup_adc(adc_clock_internal);
lcd_init();
lcd_putc("\f");

while(1) { set_adc_channel(0);
delay_ms(1);
bits=read_adc();

   tem=bits*0.4882;             
   lcd_gotoxy(1,1);            
   lcd_putc("LA TEMPERATURA");
   lcd_gotoxy(2,2);            
   printf(lcd_putc,"ES C= %f    ",tem); 
   delay_ms(1000);  
} }
