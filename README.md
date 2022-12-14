# NACA0012-Simulation

The current simulation does not predict Cd values correctly and has a very coarse mesh.

Steps to run using OpenFoam

run blockMesh <br />
run checkMesh <br />
run rhoPimpleFoam <br />
run paraFoam or postProcess command <br />
