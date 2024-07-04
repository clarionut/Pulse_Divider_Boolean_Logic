# Pulse Divider and Boolean Logic

A synthesizer module based on the original CGS36 circuit (https://sdiy.info/wiki/CGS_pulse_divider_and_Boolean_logic).

I was particularly concerned about high current consumption as the original outputs put 15V across a potential divider with a total resistance of 2.8k.
Even at Eurorack levels of 12V that's over 4mA per 'on' output, not counting the LEDs. Instead I powered the outputs from a dedicated 78L09 9V supply
(I like strong gate/trigger signals) and removed the resistor chain to ground.

The pulse divider now has a /1 output, which is a buffered copy of the incoming clock at the same voltage level as the divided outputs.

There are significant changes to the logic gates too
- the AND and OR gates have the same modification to their outputs as the pulse divider stages
- the original XOR gate can only compare signals of approximately the same voltage. I added a voltage conditioner to the input using op-amp comparators, allowing a wider range of input signals to be compared.
- the XOR comparator / output stage is an LM324 running off +9V
- the dedicated XNOR circuitry has been removed
- the NOT gates are replaced by 3 op-amp inverters using the remaining stages of the LM324, with their inputs normalled to the AND, OR and XOR outputs for maximum flexibility

For reasons of economy I built the pulse divider and Boolean logic circuits on two separate PCBs. The logic board is daisy-chained from the divider board for its power supply, and also uses two stages of the TL084 as its input voltage conditioner. To build this board as a stand-alone unit will require a redesign with power input circuitry and a TL082 as the voltage conditioner.
