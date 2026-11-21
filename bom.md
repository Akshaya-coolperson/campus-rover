CAMPUS ROVER - BILL OF MATERIALS
Course: Fundamentals of IoT and Sensors (26EC1101E)

QTY  PART                       LANE   SUPPLY                 INTERFACE
1    ESP32 DevKit               Think  5V USB / 3.3V logic    -
1    HC-SR04 ultrasonic         Sense  5V                     Trig/Echo pulses
1    DHT22 temp/humidity        Sense  3.3-6V (run at 3.3V)   Single-wire
1    LDR light module           Sense  3.3-5V (run at 3.3V)   Analog
1    HC-SR501 PIR               Sense  5V                     Digital out
1    SSD1306 0.96" OLED         Think  3.3-5V (run at 3.3V)   I2C 0x3C
1    L298N motor driver         Act    7.4V motor pack        IN1-IN4 + ENA/ENB
2    TT gear motors             Act    3-6V (from driver)     Via L298N
2    SG90 micro servos          Act    4.8-6V                 PWM
2    18650 cells (7.4V pack)    Power  7.4V nominal           -

WIRING NOTES
- HC-SR04 (classic 5V): Echo sends 5V, above the ESP32's 3.6V max.
  Fix: use a 3.3V variant (HC-SR04P / RCWL-1601) at 3.3V,
  or add a level shifter on Echo. Trig from the ESP32 is fine.
- LDR: power at 3.3V, use an ADC1 pin (GPIO 32-39). ADC2 stops
  working when Wi-Fi is on.
- OLED: I2C default pins SDA 21 / SCL 22.
- TT motors: never on a GPIO pin, they need hundreds of mA. Go
  through the L298N.
- SG90 servos: power from 5V with a shared ground, never the 3.3V
  pin. A 3.3V GPIO signal works in practice.
- Motor power (18650 pack) is separate from logic power, with
  grounds joined (Week 7).