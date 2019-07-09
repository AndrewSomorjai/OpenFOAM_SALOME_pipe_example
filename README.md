# OpenFOAM_SALOME_pipe_example
A simple example of a straight pipe with a mass flow rate.

This was tested with an AMD64 processor (32 gigs RAM)
on Xubuntu 18.04 LTS with OpenFOAM v18.06.

Open pipe_viscous.hdf in Salome (must use 7z to extract the files).

Export rotor mesh as pipe.unv into straight_pipe/

start command line in straight_pipe/

follow the steps
	
	/straight_pipe$ ideasUnvToFoam pipe.unv	
	/straight_pipe$ checkMesh
	/straight_pipe$ decomposePar
	/straight_pipe$ mpiexec -np 2 renumberMesh -overwrite -parallel

In your parallel processor files ( e.g. processor1/constant/polyMesh/boundary)
the polyMesh boundary files need to look like this for patches wall and valve.

wall
    {
        type            wall;//this will cause an error if it's not wall
        nFaces          0;
        startFace       555107;
}
	
	/straight_pipe$ mpiexec -np 2 pimpleFoam -parallel | tee log .pimpleFoam

The simulation should now run....
