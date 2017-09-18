---
ID: 3235
post_title: 'Analog pH Meter with PIC16F684  and arduino'
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/analog-ph-meter-with-pic16f684-and-arduino/
published: true
post_date: 2015-03-22 10:14:32
---
Need to measure water quality and other parameters?  DF Robot's <a href="http://www.dfrobot.com/index.php?route=product/product&amp;product_id=1025">Analog pH Meter Kit</a> is  specially designed for simple interface and has convenient and practical connector and a bunch of features. Get pH measurements at ± 0.1pH (25 ℃). For most hobbyist this great accuracy range and it's low cost makes this a great tool for biorobotics and other projects! It has an LED which works as the Power Indicator, a BNC connector and PH2.0 sensor interface. To use it, just connect the pH sensor with BND connector, and plug the PH2.0 interface into the analog input port of any micro-controller.

<a href="http://dfrobot.com/wiki/index.php/PH_meter(SKU:_SEN0161)">The Wiki page </a> has a sample code for using this kit with arduino,  along with schematic, specifications, features ,precautions and setup Instructions. The arduino Interfacing is simple and the schematic and code is available on the <a href="http://dfrobot.com/wiki/index.php/PH_meter(SKU:_SEN0161)">wiki page</a>.

<img class="aligncenter wp-image-3236 size-medium" src="http://dostmuhammad.com/wp-content/uploads/PH_meter_connection1_1-264x300.png" alt="PH_meter_connection1_(1)" width="264" height="300" />

Interfacing with a pic is also straight forward, Shawon Shahryiar shared his project where he used a PIC16F684. Below is the demonstration video and code.

https://www.youtube.com/watch?v=qwT2wIU2dkQ
<pre>
/*
Coder: Shawon Shahryiar
https://www.facebook.com/groups/ArduinoBangla/
https://www.facebook.com/groups/microarena/
https://www.facebook.com/MicroArena
 */


#include &lt;16F684.h>

#device *= 16
#device ADC = 10

#fuses NOWDT, INTRC_IO, PROTECT, PUT, CPD
#fuses NOBROWNOUT, NOMCLR, NOIESO, FCMEN

#use delay (internal = 4MHz)


#include "lcd.c"


#define const_A 0.00171016
#define LED	pin_C3


const unsigned char symbol[16] ={
    0x00, 0x1F, 0x1F, 0x1F, 0x1F, 0x1F, 0x00, 0x00,
    0x00, 0x00, 0x0E, 0x0E, 0x0E, 0x00, 0x00, 0x00
};


void setup();
void lcd_symbol();
unsigned long adc_avg();
void show_bar(unsigned char value);

void main() {
    unsigned char samples_A = 0x00;
    unsigned char samples_B = 0x00;
    unsigned long temp = 0x0000;
    unsigned long avg = 0x0000;
    unsigned long buffer[10];
    float pH_value = 0.0;

    memset(buffer, 0x00, sizeof (buffer));

    setup();

    while (TRUE) {
        for (samples_A = 0; samples_A < 10; samples_A++) {
            buffer[samples_A] = adc_avg();
            delay_ms(9);
        }

        for (samples_A = 0; samples_A < 9; samples_A++) {
            for (samples_B = (1 + samples_A); samples_B < 10; samples_B++) {
                if (buffer[samples_A] > buffer[samples_B]) {
                    temp = buffer[samples_A];
                    buffer[samples_A] = buffer[samples_B];
                    buffer[samples_B] = temp;
                }
            }
        }

        avg = 0;

        for (samples_A = 3; samples_A < = 6; samples_A++) {
            avg += buffer[samples_A];
        }

        avg >>= 2;

        pH_value = (avg * const_A);

        lcd_gotoxy(1, 1);
        printf(lcd_putc, "pH Value: %2.2g ", pH_value);
        show_bar(((unsigned char) pH_value));
    };
}

void setup() {
    disable_interrupts(GLOBAL);
    setup_WDT(WDT_off);
    setup_oscillator(OSC_4MHz);
    setup_comparator(NC_NC_NC_NC);
    setup_ADC(ADC_clock_div_8);
    setup_ADC_ports(sAN0);
    set_ADC_channel(0);
    setup_CCP1(CCP_off);
    setup_timer_0(T0_internal);
    setup_timer_1(T1_disabled);
    setup_timer_2(T2_disabled, 255, 1);
    set_timer0(0x00);
    set_timer1(0x0000);
    set_timer2(0x00);
    lcd_init();
    lcd_symbol();
    delay_ms(4000);
}

void lcd_symbol() {
    unsigned char s = 0;

    lcd_send_byte(0, 0x40);

    for (s = 0x00; s < = 0x0F; s++) {
        lcd_send_byte(1, symbol[s]);
    }

    lcd_send_byte(0, 0x80);
}

unsigned long adc_avg() {
    unsigned char samples = 4;
    unsigned long avg = 0;

    while (samples > 0) {
        read_adc(adc_start_only);
        while (!adc_done());
        avg += read_adc(adc_read_only);
        samples--;
    }
    avg /= 4.0;

    return avg;
}

void show_bar(unsigned char value) {
    unsigned char x_pos = 0;

    for (x_pos = 1; x_pos < = 16; x_pos++) {
        lcd_gotoxy(x_pos, 2);
        lcd_putc(0);
    }

    lcd_gotoxy((value + 1), 2);
    lcd_putc(1);

    output_toggle(LED);
    delay_ms(100);
} </pre></pre>