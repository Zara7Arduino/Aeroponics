# How to Control Actuators using Relay Module



## Introduction

Arduino and ESP boards are excellent choices for DIY projects that require automation, such as taking inputs from sensors and input devices like buttons, and sending output signals to actuators like motors, LEDs, and more. However, you cannot directly control high-current actuators using the GPIO pins of these microcontrollers because the digital output signals are limited to only a few milliamps of current.

This limitation is where drivers and relays come into play. Relays allow you to control high-current actuators with your microcontroller safely. In this guide, we'll learn how to choose the right relay module for controlling your actuators.

## Basics of Switching

Switching is a fundamental concept in electronics that involves controlling the flow of electricity in a circuit. The most basic types of switches are:

### Momentary Switch
A **momentary switch** is only active when pressed. It returns to its default state when released. These switches are commonly used in buttons and triggers.

### Toggle Switch
A **toggle switch** maintains its state after being activated. It flips between two positions, like on and off, and stays in the selected position until manually changed.

### SPST (Single Pole Single Throw)
An **SPST switch** has a single input (pole) and a single output (throw). It can either connect or disconnect the circuit. It’s the simplest type of switch.

### SPDT (Single Pole Double Throw)
An **SPDT switch** has a single input (pole) and two outputs (throws). It allows the circuit to switch between two outputs. SPDT switches are useful for selecting between two different paths in a circuit.

### DPDT (Double Pole Double Throw)
A **DPDT switch** has two inputs (poles) and two outputs (throws) for each pole. It allows for the control of two separate circuits, making it versatile for more complex switching scenarios.

### Normally Open (NO) Terminal
In a **Normally Open (NO)** configuration, the switch remains open until activated, at which point the circuit is completed, allowing current to flow.

### Normally Closed (NC) Terminal
In a **Normally Closed (NC)** configuration, the switch remains closed, allowing current to flow until activated, which then opens the circuit and stops the flow of current.

### Common Terminal
The **Common Terminal** is the reference point for switching between the NO and NC terminals. It's where the input power supply connects in a relay or switch configuration.

## Switching Using Relays

Relays act as electrically operated switches, using a low-power signal to control a higher-power circuit. They have the following important terminals:

### VCC Terminal
The **VCC Terminal** is the power input for the relay module, usually connected to the 5V or 3.3V pin of your microcontroller.

### GND Terminal
The **GND Terminal** is the ground connection for the relay module. It must be connected to the common ground (GND) of your microcontroller for the circuit to function properly.

### Signal (SIG) or Data Terminal
The **Signal Terminal** (SIG) is where the control signal from the microcontroller is connected. This signal determines whether the relay is activated or deactivated.

### Active High vs. Active Low Configuration
Relays can be configured as **Active High** or **Active Low**:

- **Active High:** The relay activates when the signal is HIGH (e.g., 5V).
- **Active Low:** The relay activates when the signal is LOW (e.g., 0V).

### Example Arduino Code for Switching

In controlling a relay module using Arduino, you need to connect the signal pin of the relay module to any GPIO (writeinfull) pin of the microntroller, GND or - to the mcu gnd, VCC to mcu 5V. Refer to the schematic diagram below:
![Basic-relay-arduino-circuit](assets/images/basic-relay-arduino-circuit.png) 

For the program or code.

You need to set the pin as output using ```pinMode()``` to enable writing to the pin connected with the relay

In activating or deactivating the relay you need to use ```digitalWrite()```.

In order to control the relay correctly you need to determine the configuration of your relay. Below are sample codes for controlling relay in ACTIVE HIGH and ACTIVE LOW configurations.

#### Active High Configuration
```cpp
const int relayPin = 7; // Connected to the SIG terminal of the relay

void setup() {
  pinMode(relayPin, OUTPUT);
  digitalWrite(relayPin, LOW); // Start with the relay off
}

void loop() {
  digitalWrite(relayPin, HIGH); // Turn on the relay
  delay(1000);                  // Wait for a second
  digitalWrite(relayPin, LOW);  // Turn off the relay
  delay(1000);                  // Wait for a second
}
```

#### Active Low Configuration
```cpp
const int relayPin = 7; // Connected to the SIG terminal of the relay

void setup() {
  pinMode(relayPin, OUTPUT);
  digitalWrite(relayPin, HIGH); // Start with the relay off
}

void loop() {
  digitalWrite(relayPin, LOW);  // Turn on the relay
  delay(1000);                  // Wait for a second
  digitalWrite(relayPin, HIGH); // Turn off the relay
  delay(1000);                  // Wait for a second
}
```

## Relay vs Relay Module

A **relay** is the core component that performs the switching action, but it often requires additional components like flyback diodes, transistors, and resistors to function correctly in a circuit. 
![Relay](assets/images/standalone-relay.png)

A **relay module**, on the other hand, is a pre-assembled circuit board that includes all necessary components to control the relay with a microcontroller safely. Relay modules simplify the integration of relays into your projects, providing built-in protection and easy-to-use pinouts.
![Relay Module](assets/images/relay-module.png)

## Types of Relays

### Mechanical Relay

A **mechanical relay** is a type of relay that uses physical moving parts to make or break connections. It consists of a coil, an armature, a spring, and one or more sets of contacts. When the coil is energized, the magnetic field pulls the armature, closing the contacts and completing the circuit.


**Pros:**
- **Cost:** Mechanical relays are generally inexpensive.
- **Versatility:** They can handle a wide range of voltages and currents.

**Cons:**
- **Performance:** They have slower switching speeds compared to solid-state relays.
- **Wear and Tear:** The mechanical parts can wear out over time, especially with high switching frequencies.

### Solid State Relay

A **solid-state relay (SSR)** is a type of relay that uses semiconductor devices like thyristors, triacs, or transistors instead of moving parts to switch circuits. When the control signal is applied, the SSR activates the semiconductor switch, allowing current to flow through the output.

**Pros:**
- **Performance:** SSRs offer faster switching times and are more reliable in high-frequency applications.
- **Durability:** They have no moving parts, so they are less prone to mechanical failure.

**Cons:**
- **Cost:** SSRs are generally more expensive than mechanical relays.
- **Heat Dissipation:** SSRs can generate more heat and may require heat sinks.

## How to Choose the Right Relay for Your Project

### Cost Considerations
Consider your budget when selecting a relay. Mechanical relays are cheaper, but solid-state relays may offer better performance and longer life, which could justify the higher cost in some projects.

### Availability
Choose a relay that is readily available in your local market or through online suppliers. Availability might influence your choice between mechanical and solid-state relays.

### Switching Frequency
If your project requires frequent switching, an SSR might be a better choice due to its faster response time and durability. For lower frequency switching, a mechanical relay could suffice.

### Expected Economic Life of the Prototype
Consider the lifespan of your project. If it's a short-term prototype, a mechanical relay might be more cost-effective. For long-term applications, investing in an SSR might reduce maintenance costs.

## Relays Available in the Philippine Market

- **Mechanical Relays:** Widely available, economical, and suitable for most general-purpose projects.
![Mechanical-Relay](assets/images/mechanical-relay.png)
- **Solid State Relays (SSRs):** Available but at a higher cost, ideal for projects requiring high-speed switching or higher reliability.
![solid-state-relay](assets/images/solid-state-relay.png)
- **Mechanical Relay Modules:** Common in local electronics shops, these modules provide an easy-to-use solution for controlling high-current devices with your microcontroller.
![Mechanical-Relay-Module](assets/images/mechanical-relay-module.png)
- **SSR Relay Modules:** Less common but available through specialized suppliers or online, these modules are ideal for industrial or high-performance applications.
![Solid-State-Relay-Modules](assets/images/solid-state-relay-modules.png)
