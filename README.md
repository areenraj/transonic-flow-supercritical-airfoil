# NACA0012-Simulation

The current simulation does not predict Cd values correctly and has a very coarse mesh.

Steps to run using OpenFoam

run blockMesh
run checkMesh
run rhoPimpleFoam
run paraFoam or postProcess command
