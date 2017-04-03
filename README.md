# DicomToMesh

DicomToMesh is a handy command line tool, which enables the user to automatically create a 3D mesh from a set of 2D DICOM images, a common image format used in medicine. The exported 3D format is STL.

<p align="center"><img alt="dicom2mesh" src="http://eidelen.diffuse.ch/dicomtomesh.png" width="80%"></p>

# Mesh Creation

The 3D surface mesh is computed by the marching cubes algorithm. As an input, this algorithm requires a threshold which indicates what range of voxel values should be considered. This threshold is also known as iso-value. In CT scans, the iso-value depends on the tissue (density). 

# Mesh Post-Processing Options

**Mesh reduction:** The mesh of a medical DICOM image can easily exceed 1 GB of data. Reducing the number of polygons, therefore, is a crucial feature. Reduction can be enabled by the option <code>-r X</code> where X is a floating-point value between 0.0 and 1.0. 

<p align="center"><img alt="reduction" src="http://eidelen.diffuse.ch/mesh-reduction.png" width="60%"></p>

**Mesh smoothing:** Acquired medical images contain often heavy noise. This is visible in the extracted 3D surface. Smoothing the mesh leads often to a better result. Smoothing can be enabled with the argument <code>-s</code>.

<p align="center"><img alt="smoothing" src="http://eidelen.diffuse.ch/mesh-smoothed.png" width="60%"></p>

**Remove small objects:** The resulting 3D mesh contains often parts which are not of interest, such as for example the screws of the table on which a CT scan of a patient was acquired. With DicomToMesh, you can remove objects below a certain size by adding the option <code>-e X</code> where X is a floating-point value between 0.0 and 1.0. <code>X</code> is a size threshold relative to the connected object with the most vertices. It is easy understandable with an example: The biggest connected object of the mesh has 1000 vertices. Then <code>-e 0.25</code> removes all connected objects with less than 250 vertices.    

<p align="center"><img alt="filter" src="http://eidelen.diffuse.ch/mesh-filter.png" width="80%"></p>

# Building

The software is written in C++ 11 and uses VTK 7.0. CMake is used as build-system.


# Contributors

The code was written for the medical planning and navigation library of AOT AG (http://www.aot.swiss). Since it is based on several open-source examples, I decided to make our code public as well. Hope somebody can use parts of it.

Have fun,
Adrian