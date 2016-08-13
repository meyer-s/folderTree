This page is a documentation of radiation exposure from the antenna as of 7/1/2010, revised 8/11/2010

Relevant equations, limit tables, and documentation for the calculations are from FCC OET Bulletin 65 Edition 97-01 Released August 1997 acquired from fcc.gov

 

Power density level of exposure and limits of exposure were calculated using the following two equations from OET65:

![](https://wiki.wmfo.org/@api/deki/files/42/=fccoet65-1.bmp)

![](https://wiki.wmfo.org/@api/deki/files/43/=fccoet65-2.bmp)

Where S is in mW/cm\^2

R is in cm

ERP is in mW

 

Values for variables:

Effective Radiated Power (ERP) = 125W fcc.gov record on wmfo

vertical location of antenna per wmfo public file page 9 on 8-11-2010:

*"TELREX LABS CR78-98 two sections horizontally polarized side mounted at the 85 foot
 (26 meter) level (C/R-AGL) on a 40 foot guyed rohn tower atop a 60 foot building.
 OHAG: 100 feet (30 meters) (without obstruction lighting)."*

thus min R is 25 ft or 7.62m

this value replaces the original min R estimated to be 10m, all calculations from this point have been revised for 762cm. 08-11-2010

because antenna is z directional field is attenuated.  based on google maps images of roof and estimated antenna height and distance from edge, maximum field strength is 35% of ERP  \<\<\<ANDY REFINE THIS NOTE\>\>\>

Therefore the worst case power density level of exposure is at minimum distance and maximum field.  Thus equation 8 becomes:

**Sexp** = 1.05\*.35\*125\*1000/(pi\*(762\^2)) =**0.0252 mW/cm\^2**

 

Slimit and Tave were taken from Table1 of OET65 (see fccoet65-3.bmp). For occupational/controlled exposure (locked rooftop with hazard signs) Slimit = 1 mW/cm\^2 and Tave = 6 min.  Equation 2 becomes

Texp\*0.0252 = 6 Thus **Texp = 238 min or 3.97 hr**

The meaning behind this value is provided by the following paragraph accompanying Equation 2 from OET65:

*      "For the example given above, if the MPE limit is 1 mW/cm2, then the right-hand side of
 the equation becomes 6 mW-min/cm2 (1 mW/cm2 X 6 min). Therefore, if an exposure level is
 determined to be 2 mW/cm2, the allowed time for exposure at this level during any six-minute
 interval would be a total of 3 minutes, since the left side of the equation must equal 6 (2 mW/cm2
 X 3 min). Of course, many other combinations of exposure levels and times may be involved
 during a given time-averaging interval. However, as long as the sum of the products on the left
 side of the equation equals the right side, the average exposure will comply with the MPE limit.
 It is very important to remember that time-averaging applies to any interval of tavg. Therefore, in
 the above example, consideration would have to be given to the exposure situation both before
 and after the allowed three-minute exposure. The time-averaging interval can be viewed as a
 "sliding" period of time, six minutes in this case."*

Based on this note Texp is out of a 6 minute period and therefore there is no danger to any persons working on the roof.  However, as these calculations are approximate and there may be a misinterpretation of the meaning of Texp; exposure should be limited to no more than 10 hours out of any 24 hour period in close proximity to the antenna (ie on the roof).

**Note: these calculations do not apply to anyone in direct contact with the antenna, tower, antenna feed, guy wires,  antenna grounding wire, or any other conductive materials connected to the antenna.  If contact with any such object is required or if any modifications or adjustments are to be made to any of these objects transmitter shut down is mandated.**

*
[Page Attachments](https://wiki-files.wmfo.org/Operations/Regulatory/Radiation_Exposeure)
