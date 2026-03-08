# CMOS Design and SPICE Simulation Workshop 2026

This workshop is based on understanding the working of MOS transistor. It covers the various modes of operation, some short channel effects, CMOS inverter voltage transfer characteristics, noise margin and more such parameters. Proper analysis along with simulation has also been carried out using Ngspice open source tools that uses SKY130 PDK. The instructor for this course is Kunal Ghosh Sir and Radhika Mam

## Basic Details

**Name:** Maaz Mahmood Siddique  
**College:** Netaji Subhas University of Technology  
**Email ID:** maazms999@gmail.com  
**GitHub Profile:** [maazm007](https://github.com/maazm007?tab=repositories)  
**LinkedIN Profile:** [maazm-ece-vlsi](https://www.linkedin.com/in/maazms-ece-vlsi/)


-------------------------------------------------------------------------------------------------------------------------


### Why do we need SPICE?
* SPICE is used to design a circuit and then perform various analysis like DC Analysis and Transient Analysis, to study the behaviour of the circuit when applying different input voltages
* Mainly, SPICE is used to perform the characterization of semiconductor devices. Characterization of a transistor is the process of measuring its electrical behavior to determine how it will function in a real circuit. By "sweeping" voltages and currents at the terminals, engineers create graphs called characteristic curves (e.g., input and output plots) that reveal critical performance data, such as threshold voltages, current gains, and switching limits. This data turns a physical device into a reliable mathematical model, ensuring that it meets design standards before it is used as a switch or amplifier in electronic systems
* Delay is the most important parameter in VLSI, but have you ever wondered where these delays come in the circuit? The transistor's W/L ratio plays an important role in determining the circuit's various parameters. How the W/L ratio is going to affect the speed, delay, current, and various other parameters is what we study using SPICE simulations
* There are some delays which are already defined by library or technology files based upon slew rates and capacitance values, so here SPICE helps us to verify those values by carrying out the simulation process
* Also, entire semiconductor devices work on some complex equations, and it is impractical to calculate the values of different parameters manually by putting the values in those equations. SPICE plays a crucial role here in carrying out the calculation of values  
  
## n-channel MOSFET (NMOS)
* It is a 4-terminal device, namely Source, Drain, Gate, and Body
* An n-type channel is developed in a p-type substrate

### *The following image describes the structure of NMOS*  

<image>

### Threshold Voltage
It is defined as the Gate-Source voltage required to form the channel between the Source and Drain n-type diffusion. It is generally represented by **V<sub>T</sub>**  
* *Now we will analyse various cases by changing the **V<sub>GS</sub>** voltage*  

**V<sub>GS</sub> = 0, Drain, Body, and Source are connected to GND**  
In this configuration, the circuit will behave in such a way that there are two back-to-back connected diodes between the Source and Drain region, due to which there will be no current flow, and since gate-source voltage is zero, there is no channel formed  

<image>  
  
**V<sub>GS</sub> = small positive voltage, Drain, Body, and Source are connected to GND**  
In this configuration, some positive charges will develop on the gate terminal, due to which it repels the positive charges of the substrate near the interface. As soon as the positive charges are repelled away, negative charge carriers will start attracting at the interface, and a depletion region will be formed between the substrate and negative charge carriers
  
**V<sub>GS</sub> = increase positive voltage, Drain, Body, and Source are connected to GND**   
As we increase the gate voltage, more positive charges are collected on the gate terminal; alternatively, more negative carriers are attracted towards the interface region, and the depletion width starts increasing by a significant amount. As a larger number of negative carriers are collected at the interface, this phenomenon is termed as Inversion of Channel region or **Surface Inversion or Strong Inversion**.  
  
The gate voltage at which this inversion takes place is termed as **Threshold Voltage**  
 
<image>
  
**V<sub>GS</sub> = increase more than V<sub>T</sub>, Drain, Body, and Source are connected to GND**  
If we further increase the Gate voltage above the threshold voltage, no more negative charges are left in the depletion region that can be attracted towards the channel region. So, it will start pulling the electrons from the source n+ type diffusion region, which has a large number of negative charges, and due to this, a continuous channel will be formed  
  
<image>

### Body Effect  
Ideally, the body and the source terminal are connected to GND. Now, if we apply a potential difference across the source and body terminal, **V<sub>SB</sub> = +ve voltage**, the depletion width near the source terminal increases. Also, due to positive supply, it will attract a few negative charges of the channel, due to which more gate voltage has to be applied to form the channel, which ultimately results in **increasing of threshold voltage**. The expression of threshold voltage is given as,  
<p align="center">
<img src="https://latex.codecogs.com/svg.image?V_{TH}=V_{TH0}+\gamma\left(\sqrt{2\phi_F+V_{SB}}-\sqrt{2\phi_F}\right)" />
</p>  
  
where,   
$V_{TH0}$: Threshold voltage when $V_{SB} = 0$  
$\gamma$: Body-effect coefficient  
$V_{SB}$: Source-to-body voltage  
$\phi_F$: Fermi potential  
  
<image>  
  
### Resistive Mode of Operation  
After the Strong Inversion happens, we will apply a **small positive voltage** at the drain terminal. Earlier, the entire channel had a potential of V<sub>GS</sub> across it, but, on application of V<sub>DS</sub> voltage, the potential difference across the channel will vary. It will be higher at the source end and lowest at the drain end. The effective voltage of the channel length is given by, <p align="center">
<img src="https://latex.codecogs.com/svg.image?V_{GS}-V(x)" />
</p>  
where x varies from 0  to L
  
* When we apply the positive voltage at drain terminal, the channel shape will no longer be uniform. Due to variation in effcetive voltage of channel length, **the shape of the channel gets tapered**, as shown in the below figure, 
 
<image>  
  
* From a semiconductor device point of view, there are two types of current, namely Drift Current and Diffusion Current. Drift Current is mainly due to external applied voltage, while Diffusion Current is due to the concentration gradient  
  
*Let's do the NMOS Drain Current derivation in the resistive mode of operation*  
#### Inversion Charge Density is given by:

<img src="https://latex.codecogs.com/svg.image?Q_I(x)=-C_{ox}\left[(V_{GS}-V(x))-V_T\right]" />

#### Oxide Permittivity

<img src="https://latex.codecogs.com/svg.image?\varepsilon_{ox}=3.97\varepsilon_0" />

<img src="https://latex.codecogs.com/svg.image?\varepsilon_{ox}=3.5\times10^{-11}\;F/m" />

#### Drain current is given by:

<div>
<em>Drain Current = (Velocity of Charge Carriers X Charge) over the entire Channel Width</em>
<br>
<img src="https://latex.codecogs.com/svg.image?I_D=-v_n(x)\,Q_I(x)\,W" />
</div>


#### Carrier Velocity is given by:

<img src="https://latex.codecogs.com/svg.image?v_n(x)=\mu_nE" />

<img src="https://latex.codecogs.com/svg.image?E=\frac{dV}{dx}" />

<img src="https://latex.codecogs.com/svg.image?v_n(x)=\mu_n\frac{dV}{dx}" />

#### Substituting the values

<img src="https://latex.codecogs.com/svg.image?I_D=\mu_n\frac{dV}{dx}C_{ox}\left[(V_{GS}-V(x))-V_T\right]W" />

<img src="https://latex.codecogs.com/svg.image?I_D\,dx=\mu_nC_{ox}W\left[(V_{GS}-V(x))-V_T\right]dV" />

#### Integration on both sides

<img src="https://latex.codecogs.com/svg.image?\int_0^LI_Ddx=\mu_nC_{ox}W\int_0^{V_{DS}}\left[(V_{GS}-V(x))-V_T\right]dV" />


#### Final Expression (Linear Region)

<img src="https://latex.codecogs.com/svg.image?I_D=\mu_nC_{ox}\frac{W}{L}\left[(V_{GS}-V_T)V_{DS}-\frac{V_{DS}^2}{2}\right]" />   

#### When V<sub>DS</sub> = V<sub>GS</sub> - V<sub>T</sub>  

<p align="center">
<img src="https://latex.codecogs.com/svg.image?I_D=\frac{1}{2}\mu_nC_{ox}\frac{W}{L}(V_{GS}-V_T)^2" />
</p>  
  
*This appear to be a perfect **constant current source**, but its not true because as we increase V<sub>DS</sub> above V<sub>GS</sub> - V<sub>T</sub>, depletion region near the drain region increases, and the effective channel length decreases due to which current increases, which is given by*  
  
<p align="center">
<img src="https://latex.codecogs.com/svg.image?I_D%3D%5Cfrac%7B1%7D%7B2%7D%5Cmu_nC_%7Box%7D%5Cfrac%7BW%7D%7BL%7D%28V_%7BGS%7D-V_T%29%5E2%281%2B%5Clambda%20V_%7BDS%7D%29"/>
</p>  

where λ is the Channel Length Modulation parameter  
  
> **Conclusion**  
> When V<sub>DS</sub> < V<sub>GS</sub> - V<sub>T</sub>: Linear mode of operation  
> When V<sub>DS</sub> ≥ V<sub>GS</sub> - V<sub>T</sub>: Saturation mode of operation
  
<image>

---------------------------------------------------------------------  
  
### What is a SPICE Model Parameter?  
A SPICE model parameter is a numerical value used in a transistor or device model to accurately represent how that device behaves in a circuit simulator like SPICE. Some of the LEVEL-1 SPICE Model Parameters are as follows:  

| Parameter | Meaning |
|----------|----------|
| V<sub>TO | Threshold voltage |
| K<sub>P | Transconductance parameter (μC<sub>ox) |
| GAMMA (γ) | Body-effect coefficient |
| V<sub>DSat | Velocity Saturation voltage |
| LAMBDA (λ) | Channel-length modulation parameter |  
  
### Workflow of SPICE  
  
<image>    
  
### Creating SPICE Netlist  
  
<image>  
  
Following is the spice netlist of the above circuit  
```
M1 vdd n1 0 0 nmos W=1.8u L=1.2u  
R1 in n1 55  
VDD vdd 0 2.5    
Vin in 0 2.5  
```  
### What are Corners specified in the tech files of SKY130?  
Corners refer to process-voltage-temperature variations (like TT (typical type), SS (slow slow), FF (fast fast), SF (slow fast), and FS (fast slow)) used to verify that a design works reliably under worst-case manufacturing and operating conditions  
  
<image>  
   
Now, we will simulate the above circuit using NgSpice and try to plot the Drain Current Characteristics. Following is the plot:  
  
<image>  
  
<image>  
  
* Through the simulation plot, we can clearly see that at different values of V<sub>GS</sub> voltage, the drain current is increasing by **square of (V<sub>GS</sub> - V<sub>T</sub>)<sup>2</sup>**. One can easily notice the difference between the adjacent drain current curves at different gate-source voltages  
  
<image>  
  
* Now, if we consider the lower technology nodes, but we tend to keep the W/L ratio the same, we expect that our simulation results should match. So let's analyse how the circuit behaves at lower technology nodes while keeping the W/L ratio the same  
  
<image>  
  
> **Conclsuion**  
> We noticed that for the same V<sub>GS</sub> voltage, the maximum drain current decreases by a significant amount in lower technology nodes. This happens due to the **Short Channel Effect** known as **Velocity Saturation**. Also, the lower technology nodes show the linear dependence between adjacent drain current curves  
  
* Now let's analyse the **Transfer Characterstics**. Here, we will fix the V<sub>DS</sub> voltage and sweep the V<sub>GS</sub> voltage between 0V and 1.8V. We will perform this analysis for both technologies and try to study the difference between the two characteristics  
  
<image>  
  
--------------------------------------------------  
### Velocity Saturation  
It states that at lower values of electric field, drift velocity is a linear function of electric field, but at higher electric field, the drift velocity becomes constant, and the electric field at which this happens is termed as **Critical Electric Field**. Hence, the value of drift velocity is given by,   
<p align="center">
<img src="https://latex.codecogs.com/svg.image?v_n(x)=\begin{cases}\dfrac{\mu_nE}{1+E/E_c},&E<E_c\\[6pt]v_{sat},&E>E_c\end{cases}" />
</p>  
  
Hence, the drain current equation will be changed to,  
<p align="center">
<img src="https://latex.codecogs.com/svg.image?I_D=\left(\frac{\mu_nC_{ox}}{1+\frac{V_{DS}}{E_cL}}\right)\frac{W}{L}\left[(V_{GS}-V_{th})V_{DS}-\frac{V_{DS}^2}{2}\right]" />
</p>  
  
Till now, we have come across three different formulas for drain current, which makes it harder for us to remember. Hence, we came up with the **Unified Current Model**, which is given as,  

<img src="https://latex.codecogs.com/svg.image?I_D=0\quad\text{for}\quad V_{OV}<0\quad(\text{Cutoff Mode})" />

<img src="https://latex.codecogs.com/svg.image?I_D=K_nV_{min}\left[V_{OV}-\frac{V_{min}}{2}\right](1+\lambda V_{DS})" />

<img src="https://latex.codecogs.com/svg.image?V_{min}=\min(V_{OV},V_{DS},V_{DSAT})" />  
where V<sub>OV</sub> represents Overdrive Voltage given by V<sub>GS</sub> - V<sub>T</sub>  
  
* For V<sub>min</sub> = V<sub>DSat</sub>, the current equation will be given by,  
<p align="center">
<img src="https://latex.codecogs.com/svg.image?I_D=\mu_nC_{ox}\frac{W}{L}\left[V_{DSAT}(V_{GS}-V_T)-\frac{V_{DSAT}^2}{2}\right](1+\lambda V_{DS})" />
</p>  
From the equation, we find that if we try to shift towards lower nodes, the current should increase, but actually this does not happen, because at lower nodes current reduces due to the Velocity Saturation Effect  
  
-----------------------------------------------------------------  
  
### CMOS VTC (Voltage Transfer Characteristics)  
 
* Transistor as a Switch: Gate-Source voltage plays an important role in the current flow. It can either allow a current to flow or block it.  
  
<image>  
  
<image>  
  
* When Vin = V<sub>DD</sub>, NMOS turns ON, and PMOS turns OFF, hence there will be a path from load capacitor to the GND, due to which at steady state, the capacitor will be fully discharged to GND and V<sub>OUT</sub> = 0V  
* When Vin = V<sub>SS</sub>, PMOS turns ON, and NMOS turns OFF, hence there will be a direct path from load capacitor to Supply Voltage, due to which the capacitor will start charging, and at steady state, the load capacitor will be fully charged to V<sub>DD</sub>  
  
<image>  
  
* Deducing the Drain Characteristics for NMOS and PMOS  
  
<image>  
  
Since we have deduced the load curve of NMOS and PMOS, now we will merge these curves to obtain the **Voltage Transfer Characteristics for CMOS Inverter**  
  
<image>  
  
---------------------------------------------------------  
  
### Switching Threshold of CMOS  
It is defined as the point at which CMOS devices switch their value from one steady-state level to another. It is also defined as a point at which **Vout = Vin**  
  
* The switching threshold of the CMOS Inverter mathematically is given by,  
  
$$V_m = \frac{r\,V_{DD}}{1+r}$$

$$r = \frac{K_p \, V_{dsatp}}{K_n \, V_{dsatn}}$$

$$r = \frac{\left(\frac{W_p}{L_p}\right)K_p' \, V_{dsatp}}{\left(\frac{W_n}{L_n}\right)K_n' \, V_{dsatn}}$$
  
The following image shows the switching threshold of CMOS  
  
<image>  
  
<image>  
  
* **Rise Delay (t<sub>PLH</sub>)**: Rise delay is the time required for the **output to rise from 50% of V<sub>DD</sub>** after the **input has crossed 50% of V<sub>DD</sub>** during a **low-to-high output transition**.

$$
t_{pLH} = t_{out}(50\%V_{DD}) - t_{in}(50\%V_{DD})
$$    
  
* **Fall Delay (t<sub>PHL</sub>)**: Fall delay is the time required for the **output to fall from 50% of V<sub>DD</sub>** after the **input has crossed 50% of V<sub>DD</sub>** during a **high-to-low output transition**.

$$
t_{pHL} = t_{out}(50\%V_{DD}) - t_{in}(50\%V_{DD})
$$  
  
The following image shows the transient analysis of the CMOS inverter and also involves the calculation of Rise Time and Fall Time  
  
<image>  
  
<image>  
  
<image>  
  
> **Conclusion**  
> When we increase the W<sub>P</sub> with respect to W<sub>L</sub>, the transfer characteristics curve shifts towards the right side and the switching threshold voltage increases. Also, the rise time delay falls by a significant amount, while there is a small increase in the fall time delay  
  
-------------------------------------------------------------------------------------  
  
### Noise Margin  
It is the maximum allowable noise voltage input signal can have without causing the incorrect output signal value, ensuing robust logic level, i.e., 0 or 1  
  
<image>  
  
* Any input voltage between 0 and V<sub>IL</sub> will be treated as logic low  
* Any input voltage between V<sub>IH</sub> and V<sub>DD</sub> will be treated as logic high  
* Any input voltage between 0 and V<sub>IL</sub> will have the output voltage as logic high  
* Any input voltage between V<sub>IH</sub> and V<sub>DD</sub> will have the output voltage as logic low  
* (NM)<sub>H</sub> = V<sub>OH</sub> - V<sub>IH</sub>  
* (NM)<sub>L</sub> = V<sub>IL</sub> - V<sub>OL</sub>  
* **Noise Margin = max(NM<sub>H</sub>,  NM<sub>L</sub>)**  
  
<image>  
  
Now, let's perform a SPICE simulation of the CMOS Inverter and try to calculate the Noise Margin.  
  
<image>  
  
----------------------------------------------------------------------------  
  
### Power Supply Scaling  
At lower technology nodes, the value of the power supply also reduces (low supply application) to maintain the efficient working of devices. We expect similar behaviour of our devices at lower technology nodes also. Let's simulate and try to study the results,  
  
<image>  
  
> **Advantages and Disadvantages of reducing the power supply**  
> * For lower value of voltage supply, the gain factor is large compared to higher value of supply voltage
> * For lower value of voltage supply, the energy consumption is much lesser than those operating at higher supply voltage  
> * Lower supply voltage cannot charge or discharege the load capacitance properly. Meaning the rise time and fall time will not be sufficient for the efficient working of devices, i.e., the rise time and fall time will increase which will impact the performance of device  
  
---------------------------------------------------------------------------------  
  
### Device Variation  
  
* **Etching Process:** Etching in semiconductor manufacturing is a critical, precise process used to remove unwanted material from a wafer's surface, creating intricate 3D patterns, circuits, and components. Actual mask may create an uneven or distorted channel legth or width, which will directly impact the drain current of MOS device  
  
<image>  
  
* **Oxide Thickness:** During fabrication, oxidation process may sometimes results in uneven formlation or deposition oxide layer due to which the oxide thickness changes and it will ultimately results in variation of drain current  
  
<image>  
  
* Now, let's perform some SPICE simulation and find whether these device variations actually affects the performance of CMOS Inverter  
  
<image>  
  
> **Conclusion**  
> CMOS Inverter operation is kept intact and is independent of any variation in parameter or device variation. This shows that CMOS Inverter is robust in nature and is immune to any kind of distortion that may occur. Although we increase the drive strength of PMOS at larger extent than NMOS, the shift in Switching Threshold is not much, which again proves that CMOS Inverter is robust and is not affected by even large variations