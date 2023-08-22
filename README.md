# Transonic Flow over a Super Critical Airfoil

## Introduction

Supersonic travel has always been an topic of particularly challenging difficulty in the aviation industry. The flow is extremely difficult to harness and counter as it is plagued by discontinuous shocks, oscillating phenomena and huge levels of drag. This problem took on such an infamous form that early venturings into the field led to the coining of the term the "sound barrier" because the task was deemed impossible at the time. Much of the conundrum involved in the problem is due to the presence of large shocks that develop on the wing which lead to a sudden increase in the overall drag by manipulation of the pressure field around the airfoil. This is termed as wave drag. 

The pressure after the shock exhibits a discontinuous jump which causes the flow to separate in view of the sudden and extreme pressure gradient. This futher increases the pressure drag even more. The freestream flow does not need to be supersonic for this to happen. Every airfoil has a particular Mach No. for which the drag spikes suddenly as the flow climbs across the airfoil and increases in velocity and becomes locally supersonic. The Mach No. at which the drag suddenly spikes is called the drag divergence Mach No. This regime of flow is called transonic as both subsonic and supersonic elements exist in the flow. 

## Super Critical Airfoils

Whitcomb, in his time at NASA (known as NACA at that point), worked on the supersonic problem to counter the high drag induced in aircraft. His approach was to develop an airfoil which would have a flatter suction section where the flow wouldn't accelerate. This causes the flow to reach the supersonic point farther down the wing. Also, the bottom part of the foil is more curved to induce an inverted normal shock - thus increasing lift. This concentrates the lift at the back portion of the of the airfoil. The wing also has a concave cusp after two-thirds of the chord length that produces a large majority of the thrust. 

This causes the dag divergence number of the airfoil to be higher than conventional ones as the onset of wave drag happens at higher Mach Nos. Supercritical airfoils are largely used in high speed aircraft and offer better landing and take-off performance. From the image below it can clearly be seen how the transonic airfoil has a more plateaued profile of pressure around it. 
</br>
![image](https://github.com/areenraj/transonic-flow-supercritical-arifoil/assets/80944803/7dd72c95-6d20-4a21-ab7d-ac395424e74e)
</br>
*Image taken from NASA Documentation*
</br>

## Setup 

We are aiming for transonic flow over one of the first of Whitcomb's airofils - NASA SC(2)-0714 airfoil. The Reynold's Number of the flow is $2.8 \times 10^6$ and the Mach No. is $0.77$ along with an angle of attack of $2^o$. We can create an extremely good hexahedral mesh using the polyLine utility in blockMesh. The following mesh is a C-Grid type with 6 blocks and resolved upto $y^+ = 4.5$ (calculated by the simulation). We are utilizing the K-OMega SST model that tends to be a blend between the K-Epsilon and the K-Omega Turbulence models. For this resolution, the mesh is in the viscous sub-layer and hence we can remove the use of wall functions from the simulation. OpenFOAM has its own set of lowRe wall functions that can be used for resolved meshes - we utilize them here. It is to note that using zeroGradient at the boundary resulted in approximately the same results. The chord length of the airfoil is 0.10943 and the distance from the leading edge to the starting of the domain is 0.5425. And that from the trailing edge to the outlet is 1.1. 
![mesh1](https://github.com/areenraj/transonic-flow-supercritical-arifoil/assets/80944803/64fddd94-2f8f-4c0f-a976-e402e35f7caf)
</br>
*C-Grid Mesh along the airfoil*
</br>
![mesh2](https://github.com/areenraj/transonic-flow-supercritical-arifoil/assets/80944803/6ee87368-6026-4618-bff1-1be632b0eeab)
</br>
*Mesh resolved close to the airfoil surface*
</br>

We use the solver rhoPimpleFoam that is able to handle both compressibility and turbulence. It is important to note that temperature is another field that needs to be solved over here as the density is calculated using the equation of state. We are using the solutions and schemes file of the NACA0012 tutorial that is a similar test case.
## Results

The following contours are obtained for the particular simulating case. The sonic line can clearly be seen in the Mach No. contour. Pressure waves reflect off this sonic boundary onto the airfoil surface and undergo interference with each other in this region. The flow away from this in the vicinity is subsonic.
</br>
![mach](https://github.com/areenraj/transonic-flow-supercritical-arifoil/assets/80944803/c4627226-53fe-4223-a5ab-4b35c80b6015)
</br>
*Mach Contours*
</br>
![velocity](https://github.com/areenraj/transonic-flow-supercritical-arifoil/assets/80944803/b162b22b-0dee-4701-a119-8ecd16e30cca)
</br>
*Velocity Contours*
</br>

The values of the coefficients are steady and as follows
```math
C_l = 0.978
```
```math
C_d = 0.0693
```
These values are appreciably different from that of those found in literature. The reason for such discepancy is two fold
1. The lack of resolution of $y^+ < 1$ seems to be an issue with accurracy of calculating the shear stress and the boundary layer around the airfoil.
2. The use of upwind scheme seems to be too diffusive in nature and does not do a good job of calculating the pressure field around the shock.

The use of a more resolved mesh along with more accurate and less diffusive schemes can help with the accuracy.
