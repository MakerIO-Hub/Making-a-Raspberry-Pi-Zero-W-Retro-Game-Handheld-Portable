Making a Raspberry Pi Zero W Retro Handheld Portable

Turn your Raspberry Pi Zero W retro gaming handheld into a fully portable gaming device!

In this project, we'll upgrade our previously built Raspberry Pi Zero W retro handheld by adding a rechargeable battery-powered system. The goal is to eliminate the need for an external power supply and make the handheld capable of running independently on battery power.

We'll build a compact power system using a rechargeable LiPo battery, a TP4056 charging module, an MT3608 DC-DC boost converter, and a power switch.

The system supplies regulated 5V power to the Raspberry Pi Zero W and the connected components, allowing us to enjoy retro games wherever we go.

## 🔗 Links & Project Resources

- 📺 **Previous Video – Full Handheld Build:** [Watch the Full Build & Testing Video](https://youtu.be/bb3McqdNa0c)
- 📺 **Latest Video – Making It Portable:** [Watch the Portable Power System Build](https://youtu.be/xu1qENdJqgE)

---

### PCB Design & Manufacturing

If you have a schematic but want to speed up the process of generating PCB files, you can try [JLCPCB Layout Service](https://jlcpcb.com?from=MakerIO).

Their professional engineers can turn your schematic into manufacturing-ready PCB files in as little as 3 working days. You can then use the completed PCB files to directly place an order for PCB fabrication or PCBA on JLCPCB.

If you'd like to give this service a try, why not claim a $90 Layout Service coupon first:
[Claim your $90 Coupon Center](https://jlcpcb.com/coupon-center?from=MakerIO_couponcenter)

---

# Project Overview

In the previous project, we built a retro gaming handheld using a Raspberry Pi Zero W, a 2.8-inch SPI display, physical buttons, and an audio module. However, the handheld still required an external power source. This upgrade solves that problem by introducing a rechargeable battery and a custom power management setup.

The power system has three main functions:

- **Battery Charging:** The TP4056 module charges the rechargeable lithium battery.
- **Voltage Regulation:** The MT3608 boost converter increases the battery voltage and provides a regulated 5V output.
- **Power Control:** An ON/OFF switch allows us to turn the handheld on and off.

Once everything is connected, the Raspberry Pi Zero W can boot and run RetroPie without requiring an external power supply.

# Features

- Portable battery-powered operation
- Rechargeable battery system
- USB charging through the TP4056 module
- Adjustable 5V output using the MT3608 boost converter
- Physical ON/OFF power switch
- Compatible with the existing Raspberry Pi Zero W handheld
- No external power adapter required during normal operation

# Hardware Components

Here is the list of components used to build the portable power system.

| Component              | Description                                        |
| ---------------------- | -------------------------------------------------- |
| Raspberry Pi Zero W    | Main computer running the retro gaming system      |
| ---                    | ---                                                |
| LiPo Battery           | Rechargeable power source                          |
| ---                    | ---                                                |
| TP4056 Charging Module | Charges the single-cell lithium battery            |
| ---                    | ---                                                |
| MT3608 Boost Converter | Increases the battery voltage to 5V                |
| ---                    | ---                                                |
| ON/OFF Power Switch    | Controls the power supply                          |
| ---                    | ---                                                |
| Breadboard             | Used for assembling the circuit                    |
| ---                    | ---                                                |
| Jumper Wires           | Connects the power modules and handheld components |
| ---                    | ---                                                |
| 2.8-inch SPI Display   | Displays the retro games                           |
| ---                    | ---                                                |
| Physical Buttons       | Provides gaming controls                           |
| ---                    | ---                                                |
| MAX98357A Audio Module | Handles audio output                               |
| ---                    | ---                                                |

The Raspberry Pi Zero W, display, buttons, and audio hardware are part of the original handheld build. This project focuses on adding the portable power system.

# Understanding the Power System

Before connecting the components, it is important to understand how the power system works. The battery provides the energy required to operate the handheld. However, its voltage is not suitable for directly powering the Raspberry Pi Zero W. That's why we use two additional modules.

## 1. Rechargeable LiPo Battery

The battery is the main power source of our portable handheld. It stores the electrical energy needed to run the Raspberry Pi and its connected components. Since the battery voltage changes depending on its charge level, we need a voltage converter to provide a stable supply to the system.

## 2. TP4056 Charging Module

The TP4056 is a charging module designed for single-cell lithium-ion and lithium-polymer batteries. It allows us to recharge the battery through its USB charging input. The battery connects to the module's battery terminals, while the protected output terminals, when available on the specific board version, can provide power to the rest of the circuit.

Important: TP4056 boards are available in different versions. Check the terminal labels and protection circuitry on your exact module before connecting the battery and load.

## 3. MT3608 Boost Converter

The MT3608 is a DC-DC boost converter. Its job is to increase the battery voltage to the 5V required by the Raspberry Pi Zero W. The output voltage can be adjusted using the onboard potentiometer. Before connecting the Raspberry Pi, the output must be adjusted and measured with a multimeter to ensure it is stable and correctly set to 5V.

## 4. ON/OFF Power Switch

The physical power switch allows us to control the power supplied to the handheld. When the switch is turned on, the battery-powered circuit supplies power to the boost converter, which provides the regulated 5V output to the Raspberry Pi and the connected hardware. When the switch is turned off, the system stops receiving power from the battery through this circuit.

# Wiring and Connections

The general power flow of the system is:  
Battery → TP4056 Charging Module → Power Switch → MT3608 Boost Converter → 5V Power Rails → Raspberry Pi Zero W

The TP4056 handles battery charging, while the MT3608 provides the regulated voltage required by the handheld.

## Power System Connections

| Connection                       | Purpose                                                                           |
| -------------------------------- | --------------------------------------------------------------------------------- |
| Battery Positive                 | Connects to TP4056 B+                                                             |
| ---                              | ---                                                                               |
| Battery Negative                 | Connects to TP4056 B-                                                             |
| ---                              | ---                                                                               |
| TP4056 Protected Output Positive | Supplies the boost converter through the power switch, if the board provides OUT+ |
| ---                              | ---                                                                               |
| TP4056 Protected Output Negative | Connects to the boost converter input ground, if the board provides OUT-          |
| ---                              | ---                                                                               |
| Power Switch                     | Controls the positive supply path to the boost converter                          |
| ---                              | ---                                                                               |
| MT3608 IN+ / IN-                 | Receives battery power                                                            |
| ---                              | ---                                                                               |
| MT3608 OUT+ / OUT-               | Provides regulated 5V output                                                      |
| ---                              | ---                                                                               |
| 5V Power Rail                    | Distributes 5V to the handheld                                                    |
| ---                              | ---                                                                               |
| GND Power Rail                   | Provides the common ground connection                                             |
| ---                              | ---                                                                               |

## Connecting the Raspberry Pi

The regulated output from the MT3608 is distributed through the breadboard's power rails.

- MT3608 OUT+ connects to the positive 5V rail.
- MT3608 OUT- connects to the ground rail.
- The Raspberry Pi Zero W receives 5V and GND from these rails.
- The display and other connected components receive power through their existing connections.

All components powered by this system must share a common ground.

**Important:** The Raspberry Pi's 5V GPIO power connection bypasses some of the protection provided by its normal USB power input. Always verify the output voltage and polarity before connecting the board.

# Assembly Process

The build is completed in several stages.

## Step 1 – Prepare the Components

Gather the battery, TP4056 charging module, MT3608 boost converter, power switch, breadboard, and connecting wires. Check the terminals and identify the positive and negative connections on each module.

## Step 2 – Connect the Battery to the Charging Module

Connect the battery to the TP4056 module using the correct battery terminals. Make sure the polarity is correct before proceeding.

## Step 3 – Connect the Power Switch

Add the ON/OFF switch to the positive power path between the charging module's protected output and the boost converter input, provided the TP4056 board supports this connection. This allows us to control the power supplied to the rest of the circuit.

## Step 4 – Connect the MT3608 Boost Converter

Connect the input terminals of the MT3608 to the battery supply. Adjust the converter output to 5V using a multimeter before connecting it to the Raspberry Pi. Never connect the Raspberry Pi before verifying the output voltage.

## Step 5 – Connect the Power Rails

Connect the positive and negative output wires from the power system to the corresponding breadboard power rails. These rails distribute power to the Raspberry Pi Zero W and the other connected components.

## Step 6 – Complete the Wiring

Connect the remaining power wires from the display and other components to the appropriate power rails. Double-check the wiring and make sure there are no loose connections or accidental short circuits.

## Step 7 – Power On and Test

Once all connections are complete, turn on the system using the physical power switch. The Raspberry Pi Zero W should begin its normal boot sequence. The display may initially show a white screen. This is normal during the startup process. Afterward, the Linux boot messages appear, followed by the RetroPie interface.

# Testing the Portable Handheld

After completing the wiring, it is time to test the system. First, we turn on the power switch and check whether the Raspberry Pi Zero W starts correctly. During startup, the display initially shows a white screen. After a short wait, the Linux boot messages appear, followed by the RetroPie logo.

Once the system has finished booting, we launch Super Mario World to test the handheld. The game runs successfully, and the audio output works as expected. This confirms that the portable power system can supply the Raspberry Pi Zero W and its connected hardware during operation.

# Important Safety Notes

Working with rechargeable lithium batteries requires care. Please keep the following points in mind:

- Always verify battery polarity before making connections.
- Use a compatible charging module for your battery chemistry and cell configuration.
- Check whether your TP4056 board includes battery protection circuitry.
- Do not assume every TP4056 module has protected output terminals.
- Adjust the MT3608 output to 5V and verify it with a multimeter before connecting the Raspberry Pi.
- Avoid short circuits between the positive and negative power rails.
- Use suitable wires and secure connections for the expected current.
- Do not leave a lithium battery charging unattended.
- Never charge a damaged or swollen battery.
- Make sure the battery and power modules have adequate ventilation and are not overheating.

**Note:** The TP4056 is intended for single-cell lithium batteries. This circuit should not be used with a multi-cell battery pack without an appropriate charging and protection system.

# Project Files

The complete project documentation and wiring schematic are available in this GitHub repository.

- Wiring Schematic: File
- Project Documentation: File
- Previous Handheld Build: File

# Final Result

With this upgrade, our Raspberry Pi Zero W retro gaming handheld is no longer dependent on an external power supply. By combining a rechargeable battery, a TP4056 charging module, an MT3608 boost converter, and a physical power switch, we have created a portable power system that allows the handheld to run independently.

Now we can power on the device, launch RetroPie, and enjoy classic games like Super Mario World without being connected to an external power adapter.

The handheld is now portable!

