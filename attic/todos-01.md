# TODOs for -01

## Introduction
- Here is a list of potential TODOs for -01 (collected from the various sources of feedback on -00):
- Upon evaluation, the information presented herin, might be useful for the eimpact-icmp document.
- The lines marked with "T" are what are current TODOs and ones with "[ ] or [x]" are checkboxes, representing their status.

## Final TODOs
1. [ ] Ask Ron what elements from the -ivy- draft he would want in.
2. [ ] Find for a way to identify a component, and then the power of it. (like in ivy-power's S2.a). This can be another C-Type
3. [x] Add the discussions about the validity and integrity of the data sent from one node to another.
4. [x] Check about ADs (check the applicability of https://datatracker.ietf.org/doc/draft-wkumari-intarea-safe-limited-domains/)
5. [ ] Mention something about what transports are being used to convey the metrics? (YANG was preferred in the interim). [Directly mention 'ICMP carrying the metrics based on a YANG model' and discuss different choices of transport]

## Potential Use cases (for future):
1. For power consumption sub-object:
    - This sub-object can be used to take action on the S2.b, S2.c and S2.d (components)
    - S5.a and S5.b from -ivy-power can be used as a use case for the Power Comsumption sub-object. i.e., we can use the pow. consump. sub-object and based on the I/P or O/P B/W expectations and average power consump.(^), the action can be taken to put the device to power-save or not.
    
      (^) This can either be calculated based on multiple readings or just fetched from the node.
    - Another use case is to power down / send more traffic to a low power consuming node.
    - If low/high power consuming node, there can be a use case to turn it down. But before turning it down, are we looking at the recourse utilization? It might be possible that the device might be processsing high/low amount of traffic whilst being efficient/inefficient. So, I believe that we also might have to include an extra variable (like utilization) when considering the use case for the power consumption.