Chapter 10 Potentiometer & LED
================================
Earlier we have learned the use of ADC and PWM. In this chapter, we will learn 
how to use a potentiometer to control the brightness of an LED.

Project 10.1 Soft Light
------------------------
In this project, we will make a soft light. We will use an ADC Module to read ADC 
values of a potentiometer and map it to duty cycle of the PWM used to control the 
brightness of a LED. Then you can change the brightness of a LED by adjusting the 
potentiometer.

Component List
^^^^^^^^^^^^^^^
- ESP32-S3-WROOM x1
- GPIO Extension Board x1
- 830 Tie-Points Breadboard x1
- Resistor 220Ω x1
- Potentiometer(10k) x1
- LED x1
- Jumper Wire x5

Connect
^^^^^^^^^^^

.. image:: img/connect/10.1.png

Sketch
^^^^^^^
**Sketch_10.1_Softlight**

.. image:: img/software/10.1.png

Download the code to ESP32-S3 WROOM, by turning the adjustable resistor to change 
the input voltage of GPIO19, ESP32-S3 changes the output voltage of GPIO14 according 
to this voltage value, thus changing the brightness of the LED.

Code
^^^^^^
The following is the program code:

.. code-block:: C

    #define PIN_ANALOG_IN   1
    #define PIN_LED         14
    #define CHAN            0
    void setup() {
    ledcAttachChannel(PIN_LED, 1000, 12, CHAN);
    }

    void loop() {
    int adcVal = analogRead(PIN_ANALOG_IN); //read adc
    int pwmVal = adcVal;        // adcVal re-map to pwmVal
    ledcWrite(PIN_LED, pwmVal);    // set the pulse width.
    delay(10);
    }

In the code, read the ADC value of potentiometer and map it to the duty cycle of 
PWM to control LED brightness.
