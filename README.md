# Minimal RP2040 DC Motor Controller

This tscircuit project defines a compact carrier board for a single brushed DC motor.

## Selected inventory parts

- Seeed Studio XIAO RP2040: USB-programmable microcontroller module used by this board.
- Adafruit DRV8833 DC / Stepper Eval Board: H-bridge motor driver module for PWM speed and direction control.
- 0.1in 2.54mm Screw Terminal 2 Pin: motor supply input and motor output terminals.
- Breakable Male Headers / 90 degree female 0.1in headers: module sockets for the XIAO RP2040 and DRV8833 breakout.
- Cap 10uF 0805: bulk motor-supply capacitor.
- Cap 0.1uF 0603: high-frequency motor-supply bypass capacitor.
- Red LED 1608: power indicator.
- Resistor Array 4 1206 or an available 0603 resistor: LED current limiting.

## Control wiring

- XIAO D8 / GPIO2 -> DRV8833 AIN1
- XIAO D10 / GPIO3 -> DRV8833 AIN2
- XIAO D9 / GPIO4 -> DRV8833 SLEEP
- XIAO D7 / GPIO1 <- DRV8833 FAULT
- Arduino shield VIN / barrel-jack input -> DRV8833 VMOTOR
- VMOTOR terminal -> DRV8833 VMOTOR, as an alternate/direct motor supply input
- MOTOR terminal -> DRV8833 AOUT1/AOUT2
- Arduino shield V5 -> XIAO 5V logic power through `ArduinoShield` `chipProps.connections`
- Arduino shield GND1 -> common GND through `ArduinoShield` `chipProps.connections`
- All grounds are common.

## Adafruit DRV8833 socket

The Adafruit DRV8833 breakout is represented as two female header rows:

- `J_DRV8833_LEFT`: VMOTOR, GND, FAULT, BIN1, BIN2, SLEEP, AIN2, AIN1
- `J_DRV8833_RIGHT`: BSEN, ASEN, BOUT1, BOUT2, AOUT2, AOUT1

The two rows are spaced 17.00 mm center-to-center per the requested mechanical layout.

## Seeed Studio XIAO RP2040 socket

The Seeed Studio XIAO RP2040 footprint is represented as two 7-pin female header rows:

- `J_XIAO_LEFT`: D0/A0/GPIO26, D1/A1/GPIO27, D2/A2/GPIO28, D3/A3/GPIO29, D4/SDA/GPIO6, D5/SCL/GPIO7, D6/TX/GPIO0
- `J_XIAO_RIGHT`: D7/RX/GPIO1, D8/SCK/GPIO2, D9/MISO/GPIO4, D10/MOSI/GPIO3, 3V3, GND, 5V

The two rows are spaced 20.00 mm center-to-center in this carrier board per the requested mechanical layout. Seeed's official KiCad PCB source places the XIAO's own two `H7-HALF-HOLE-2.54` header footprints 15.24 mm apart, so this board intentionally uses a wider socket spacing than the stock XIAO module.

## Notes

The raw DRV8833RTYR IC was not selected for the first minimal board because it needs exact support parts around VINT, VCP, VM, and current-sense pins. The Adafruit DRV8833 eval board already includes the motor-driver IC and its required local passives, making the carrier board smaller and less risky with the listed inventory.
