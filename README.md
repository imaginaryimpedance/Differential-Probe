# Differential-Probe
 Purpose of this project was to design low cost differential probe with attenuations of x10 and x100 
 to measure voltages up to 1kV with bandwidth of atleast 10MHz. Theorethical bandwidth of this probe is estimated at 100MHz
 according to LTSpice. Testing only proved bandwidth of 25MHz as it is limited by Analog Discovery 2 network analyzer max frequency. 
 

## Design description
Device is based on AD8130 differential amplifier and THS3491 amnplifier on output stage.

![LTSpice Bandwidth](Simulations/Simulation_sch.png)

Bandwidth according to simulation is above 100MHz:
![LTSpice Bandwidth](Simulations/BW_x100.png)

CMRR is 65dB in worst case, 140dB for DC and frequencies below 20kHz:
![LTSpice Bandwidth](Simulations/CMRR_Plot.png)

Gain of the amplifying stage is constant at 10. Attenuation is switched between 1000 and 100 by relay.

Input protection is done by 1N4148 diodes connected to resistor dividers at 3V, as maximum input voltage for AD8130 is 8.4V, so protection diodes cannot use power rails

![LTSpice Bandwidth](Simulations/AD8130_max_ratings.png)


![LTSpice Bandwidth](Simulations/Input_protection_sch.png)
![LTSpice Bandwidth](Simulations/Input_protection_Plot.png)

## Bring up

### Power rails

### DC Attenuator

To achieve even attenuation for positive and negative input, remove resistor R137 and R138, force DC voltage floating from probe power supply ground and adjust potentiometers RV101 for x10 and RV102 for x100 so voltages between GND and test points TP103 and TP104 are equal. 

### AC attenuator 

Using device with Bode Plot funcionality, for example Analog Discovery 2, connect generator to positive input and coaxial shield to negative, and adjust variable capacitors on positive side of attenuator for flat frequency response:

Example of unadjusted probe
![LTSpice Bandwidth](Simulations/x100_Bode_before_cal.png)

After adjusting:
![LTSpice Bandwidth](Simulations/x100_Bode_after_cal.png)


Note: AD2 max bandwidth is 25MHz, so 
![LTSpice Bandwidth](Simulations/AD2_Bode_base_plot.png)

On this step, 5MHz output filter can also be checked and adjusted

### Offset trim

Short positive and negative inputs and connect DMM to the output. Adjust potentiometer RV103 to achieve near-zero offset.


