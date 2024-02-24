Here is a list of potential TODOs for -01 (collected from the various sources of feedback on -00):

Upon evaluation, the information presented herin, might be useful for the eimpact-icmp document.

The lines marked with "T" are what are current TODOs and ones with "[ ] or [x]" are checkboxes, representing their status.

1. Go through Ron's YANG Models for useful metrics and units (draft-li-ivy-power)
    Powering off portions of network elements could save a significant amount of power, but to scale and be practical, this must be automated.

    S2. Power Management elements:
      - a. Power Comsumption            (used-power)                    (uint32, Power drawn by COMPONENT{watts}, leaf node)
      - b. Power control capability     (power-save-capability)         (boolean, True if component can be put to power save, leaf node)
      - c. Power control                (power-save)                    (boolean, True if component is in power save mode, leaf node, R/W)
      - d. Automatic Power Management   (automatic-power-management)    (boolean, True if component is regulating its own power, leaf node, R/W)

    S3. Functional Dependencies
        This doc also suggests functional dependencies which might also be useful for us, we can reference this doc?

    S5. Traffic Planning
      - Some systems have the capability of automatically managing their power consumption if they have an understanding of the expected traffic loads. To provide this, we provide the expected input and output bandwidth for each interface and augment [RFC7223]
        - a. expected-input-banwidth      (uint32, exp. input B/W of the interface{Mbps}, 0 = full B/W, leaf node, R/W)
        - b. expected-output-bandwidth    (uint32, exp. output B/W of the interface{Mbps}, 0 = full B/W, leaf node, R/W)

    **What is in for eimpact-icmp?**
      - **T1. As we already have defined a "NODE LEVEL" Power Comsumption sub-object, we can reference S2.a.**
        **T2. Use case of this: This sub-object can be used to take action on the S2.b, S2.c and S2.d (components)**
      - **T3. S5.a and S5.b can be used as a use case for the Power Comsumption sub-object.**
        **i.e. we can use the pow. consump. sub-object and based on the I/P or O/P B/W expectations and average power consump.(*), the action can be taken to put the device to power-save or not.**
        **(*) This can either be calculated based on multiple readings or just fetched from the node.**
      - **T4. Another use case is to power down / send more traffic to a low power consuming node.**

2. Go through Michael's suggestions
    - Shift/move traffic from more-power consuming path (this can be good savings once compounded by multiple devices)
    - Metrics:
      - Power/byte or power/packet?
      - Idle power (we can make a section in the power consumption sub-object to include idle power?)

    **What is in for eimpact-icmp?**
      - **T5. Potential use cases that we can think about**

3. Go through Ron's suggestions
    - Use case is to power down / send more traffic to a low power consuming node.

    **What is in for eimpact-icmp?**
      - **T6. Potential use cases that we can think about**

4. Go through Jari's suggestions
    - [x] What type of transports can be used for conveying sustainability-related info. And why.
      E.g., lots of data, little data, IP level (ICMP), an app-level, part of a bigger e.g. device YANG data framework and associated transport protocols, etc.
      (YANG level was preferred during the interim)
    - [ ] Discuss the validity and integrity of the data sent from one node.
    - [x] Single AD or across ADs?
      Answer: particularly the single admin domain versus broader needs to be covered.
    - [ ] Security considerations
    - [x] discuss choice of transport icmp vs other things (eg management)

    - TODO NITS:
      - [x] Informtation Object and not impact object (Impact .. means eg that we took renewable usage into account etc.)
      - [x] The defined object doesn’t say it is per node, you only find that out in the “other” section
      - [x] the other metrics could be aligned better in terms of units so that we understand how they differ and what’s included
      - [ ] many of these things are difficult to define exactly eg idle power… how idle do you want? With what shut off, or just no traffic flowing? Typically there are many levels of idleness w or wo implications
      - [x] you should probably say right from get go that this info is for within admin domain or else there’s no way to say the data is valid in any way

    **What is in for eimpact-icmp?**
      - [ ] **T7. We need to mention what transports are being used to convey the metrics? (YANG was preferred in the interim).**
        **So, can we directly mention 'ICMP carrying the metrics based on a YANG model' or discuss different choices of transport?**
      - [ ] **T8. Discuss things about integrity and validity and considerations in the security section**
      - [x] **T9. Add details stating single admin domain**
      - [x] **T10. Correct the NITS**

5. draft-cparsk-eimpact-sustainability-considerations -- Sustainability Considerations for Internetworking
    **What is in for eimpact-icmp?**
      - **T11. Carbon intensity (CI):**
        **grams of carbon-equivalent per kilowatt hour (gCO2e/KWh).**
      - **T12. CUE or PUE:**
        **Carbon usage effectiveness [CUE] is a metric that helps determine the amount of greenhouse gas (GHG) emissions produced per unit of IT energy consumed within a data center (ratio of the total CO2 emissions caused by total data center energy consumption, divided by the energy consumption of IT equipment)**
    
6. draft-cx-opsawg-green-metrics -- Green Networking Metrics
    - Section 3 (Green Metrics)
      This section categorizes green metrics according to the subject of the metrics:
      - Device Level*
      - Flow Level
      - Path Level
      - Network Domain Level*
      (*) We have used these two categories in this draft

      For example, a primary metric might be the power consumption of a device, while a derived metric might be a metric that relates energy consumption to utility provided, for example power consumption per gB of traffic passed. In general, instrumentation will focus on primary metrics that need to be measured where they occur, while derived metrics can be computed from other metrics.
      An example would be metrics that convert energy use into carbon footprint, using a formula to compute emitted CO2 based on energy use using some factor.  Another example would involve the use of sustainability factors that reflect the energy mix used to power a given piece of equipment, resulting in metrics reflecting discounted energy use based on those factors.

      3.1.1: Energy Consumption Metrics
      They also provide a good proxy to model expected actual energy use in a network.
      * Power consumption when idle (e.g., Watts)
      * Power consumption when fully loaded (e.g., Watts)
      * Power consumption at various loads: e.g., power consumption at 50% utilization, power consumption at 90% utilization
      
      These metrics should be maintained for the device as a whole, and for the subcomponents, i.e.:
      * For the chassis by itself
      (I have added just those which we can use for now)

      **What is in for eimpact-icmp?**
        - **T13. Describe something more about device level green metrics?**
        - **T14. Add some use case scenarios on how we can use the metric or how one metric can be used several ways (idle, fully loaded,various load etc)**

T16. Can we use temperature?
T17. Another scenario: We have two scenarios: If low/high power consuming node, there can be a use case to turn it down. But before turning it down, are we looking at the recourse utilization? It might be possible that the device might be processsing high/low amount of traffic whilst being efficient/inefficient. So, I believe that we also might have to include an extra variable (like utilization) when considering the use case for the power consumption. 