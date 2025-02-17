# CMOS Temperature Sensor Design in 180nm

## Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Design and Implementation](#design-and-implementation)
  - [Self-biased PTAT Generator with Startup Circuit](#1-self-biased-ptat-generator-with-startup-circuit)
  - [10-bit SAR ADC](#2-10-bit-sar-adc)
  - [Additional Circuit Blocks](#3-additional-circuit-blocks)
    - [Comparator](#comparator)
    - [Digital-to-Analog Converter (DAC)](#digital-to-analog-converter-dac)
- [Applications](#applications)
- [References](#references)

## Overview
This project focuses on designing a high-precision CMOS temperature sensor for an IoT system. The sensor PTAT Generator circuit with high-order curvature correction and a 10-bit SAR ADC to convert temperature variations into digital signals. The design operates within a temperature range of -40°C to 125°C with an accuracy of ±1°C, ensuring reliable performance in diverse environmental conditions.

### Key Components:
- **Temperature Sensing Stage:** Self-biased BGR with a startup circuit.
- **Analog Signal Processing block:** It ensures the signal is within the proper range for analog-to-digital conversion
- **10-bit SAR ADC:** Converts the sensed analog temperature signal into digital form.
  
![block_new](https://github.com/user-attachments/assets/6ab8393f-81a1-4bd5-a591-ae280111c916)




## Features
- **High Accuracy:** ±1°C over a wide temperature range (-40°C to 125°C).
- **Self-biased BGR:** Ensures stable reference voltage with startup circuitry.
- **High-order Curvature Correction:** Improves temperature measurement accuracy.
- **Low Power Consumption:** Optimized for IoT applications.
- **Compact Design:** Suitable for integration in small sensor modules.

## Design and Implementation

### 1. Self-biased PTAT Generator with Startup Circuit
The PTAT circuit is implemented in 180nm CMOS technology and includes a startup circuit to ensure reliable operation. It generates a Proportional-To-Absolute-Temperature (PTAT) voltage that serves as the temperature-dependent reference. This section shows the schematic and simulation results for this crucial block.

#### Schematic Diagram
Below is the schematic diagram of the PTAT generator with the startup circuit:
![Schematic Diagram](https://github.com/user-attachments/assets/ea943e14-c43c-44d8-83c1-bf43fdf86695)

#### Simulation Results
- **Plot 1: VPTAT vs. Temperature**  
  This plot illustrates how the PTAT voltage varies with temperature across different process corners (TT, FF, SS).  
  ![VPTAT vs. Temperature](https://github.com/user-attachments/assets/75892cc6-c4fc-423b-8150-84b5c7464279)

- **Plot 2: Startup Circuit Response**  
  This plot demonstrates the startup performance of the circuit.  
  ![image](https://github.com/user-attachments/assets/f6e3b2e7-bf05-4e7f-b01d-3cb03dda7199)


### 2. 10-bit SAR ADC
The SAR ADC converts the analog temperature-dependent voltage into a 10-bit digital output. It is chosen for its low power consumption, compact size, and high resolution.

#### D-Flip Flop Design
The D-Flip Flop is a key element in the SAR logic, providing storage for the binary conversion process.  
![D-Flip Flop Design](https://github.com/user-attachments/assets/ac76bdca-afd7-425e-8953-b2da08adf016)

#### SAR Logic
The SAR logic controls the ADC operation by performing a binary search to determine the correct digital output corresponding to the input voltage.  
![SAR Logic](https://github.com/user-attachments/assets/c6e3d139-ef97-44da-8e33-0086dc17de69)

#### SAR ADC
The Analog-to-Digital converter is implemented using a Successive Approximation Register(SAR) for all conversions. This design was chosen because it requires minimal logic and space on the chip.

![image](https://github.com/user-attachments/assets/42df3eb5-407c-4c92-b462-7baf59abc994)

#### Simulation Results
- **SAR Block Output:**  
  The following plot shows the output of the SAR block when the input voltage (Vin) is 0.9V.  
  ![SAR Block Output](https://github.com/user-attachments/assets/12b13c16-965a-4913-bd8f-dfef2de3de64)

### 3. Additional Circuit Blocks

#### Comparator
The comparator compares the output of the PTAT circuit with a reference voltage to facilitate the ADC's binary decision-making. It is designed with low offset, high DC gain, and stable performance across temperature variations.

![Comparator Circuit](https://github.com/user-attachments/assets/35b8a7cf-2c28-4340-b3fd-bfa0e64b93e9)

##### Simulation Results
- **Comparator Transient Response:**  
  The transient response plot below highlights the comparator’s performance under dynamic conditions.  
  ![image](https://github.com/user-attachments/assets/17eb0505-4569-4c24-91da-ceafbf943ddb)


#### Digital-to-Analog Converter (DAC)
The 10-bit DAC is implemented using an R-2R resistor network, ensuring high linearity and accuracy. It converts the digital output from the SAR ADC into an analog voltage.

- **Configuration:**  
  The DAC takes inputs from a 10-bit register, setting each bit to either **Vdd** or **ground**.
- **Resistor Specification:**  
  **R = 100kΩ**

Below is the schematic for the DAC:
![image](https://github.com/user-attachments/assets/61d1252b-889b-4968-aff5-509d37bd4a19)

#### MUX Design
A multiplexer (MUX) is used within the DAC block to select the appropriate signal path.  
![image](https://github.com/user-attachments/assets/34257a68-db41-4b58-b6f1-3d6039e4483e)


##### Simulation Results
- **DAC Output:**  
  The output plot of the DAC is shown below, confirming the expected voltage levels.
  ![DAC Output](https://github.com/user-attachments/assets/03235c65-dcfa-42cc-b370-8bb62d10de51)

#### Final Circuit Overview
The final circuit integrates the PTAT generator, SAR ADC, comparator, and DAC into a cohesive temperature sensor design.
![image](https://github.com/user-attachments/assets/f22396cc-725e-4f90-aa64-98acc9dcfd12)


**Results:**
Below is the waveform which represents the transient simulation of a SAR ADC. The step-like transitions indicate the successive approximation process, where the ADC determines each bit sequentially. The periodic pattern shows the sampling and conversion cycles in operation.

![image](https://github.com/user-attachments/assets/d8f4461e-f1e9-4755-ab41-cf3da110b292)


## Applications
- **IoT-Based Temperature Monitoring Systems**
- **Industrial and Automotive Temperature Sensing**
- **Wearable Health Monitoring Devices**
- **Environmental and Weather Monitoring Systems**

## References.
SAR-ADC Design :  https://github.com/muhammadaldacher/Analog-Design-of-Asynchronous-SAR-ADC

Temperature Sensor Reference :  https://ece.umaine.edu/wp-content/uploads/sites/203/2012/05/SPesut_ECE547.pdf


