## Notes
### Introduction
To transmit binary data over a transmission line, it must be converted to binary signals. For example, by applying *+V* volts to the sending end for 1, and *-V* for 0. Then, the receiving device can interpret +V as 1 and -V as 0. 
In practice, signals are **attenuated** (reduced), and **distorted** (misshapen) by the transmission medium. These two are strongly influenced by: a) the type of transmission medium, b) the bit rate of the data being transmitted, and c) the distance between the two communicating devices.

As attenuation and distortion can be quantified for different types of transmission media and physical separations, international standards have been defined for the electrical interface between two items of data communication equipment, defining not only the electrical signal levels to be used, but also the use and meaning of any additional control signals and conventions that are used at the physical interface. These bodies: ITU-T (Europe) and EIA (US).

### 2.1 Transmission media
The type of transmission medium is important, since it determines the maximum number of bits that can be transmissed per second (bps, or bit rate).

#### 2.1.1 Two-wire open lines
The simplest transmission medium. Each wire is insulated from the other and both are open to free space. This type of line is adequate for connecting equipment that is up to 50m[^1] apart, using moderate bit rates (less than, say, 19.2 kbps[^2]). 
The signal, typically a voltage or current level relative to some ground reference, is applied to one wire, while the ground reference is applied to the other.

Can be used to connect two DTEs directly, but mainly used for connecting a DTE to local DCE (eg a modem). This type of connection usually uses multiple lines, the most common arrangement being a separate insulated wire for each signal, and a single wire for the common ground reference. The complete set of wires is then either enclosed in a single protected **multicore cable** or molded into a **flat ribbon cable**.

Be careful of cross-coupling (called **crosstalk**). The open structure of the wires makes it susceptible to picking up noise signals from other electrical signal sources. This becomes a problem if one wire picks up the signal, and not the others - since the signal is interpreted as the difference between the voltage across both wires.

#### 2.1.2 Twisted-pair lines
Safer against spurious noise because the signal and ground wires are twisted together, meaning they'll both pick up any interference, reducing the total difference in the signal. Further, if multiple twisted pairs are enclosed in the same cable, the twisting of each pair reduces crosstalk. 

Suitable (with appropriate line driver and receiver circuits that exploit the potential advantages by using such a geometry) for bit rates in the order of 1 Mbps over short distances (less than 100m) and lower bit rates over longer distances. More sophisticated driver and receiver circuits enable similar or even higher rates over much longer distances. Such lines (unshielded twisted pairs (UTPs)) are used for telephones, and (with special integrated circuits) for data communications. With shielded twisted pairs (STPs) a protective scree or shield is used to reduce further the effects of interference signals.


## Specifics
[^1]: Max good distance for two-wire open line
[^2]: Max good bit rate for two-wire open line ("moderate")

## Exercises
2.1 Give a brief description of the application and limitations of the following types of transmission media: a) Two wire open lines, b) Twisted-pair lines, c) Coaxial cable, d) Optical fiber, e) Microwaves

2.2 With the aid of sketches, explain the differences between the following transmission modes used with optical fiber: a) Multimode stepped index, b) Multimode graded index, c) Monomode

2.3 The maximum distance between two terrestrial microwave dishes, *d*, is given by the expression:
$d = 7.14 \sqrt{Kh}$
where *h* is the height of the dishes above ground and *K* is a factor that allows for the curvature of the earth. Assuming $K = 4/3$, determine *d* for the seleccted values of *h*.

2.4 With reference to figure 2.5(b), determine the frequency assignments for a cellular system assuming a 7-cell repeat pattern. Explain the advantages of this over the 3-cell repeat pattern shown in the figure.

2.5 With the aid of sketches, explain the effect on a transmitted binary signal of the following: a) attenuation, b) limited bandwidth, c) delay distortion, d) line and system noise

2.6 Use the integrals listed in Section 2.2 to derive the Fourier series for a periodic binary signal assuming a) unipolar and b) bipolar encoding

2.7 Explain why the binary sequence 101010... is referred to as the worst-case sequence when deriving the minimum bandwidth requirements of a channel

2.8 Derive the minimum channel bandwidth required to transmit at the following bit rates assuming (i) the fundamental frequency only and (ii) the fundamental and third harmonic of the worst-case signal are to receive: a) 500bps, b) 2000bps, c) 1 Mbps