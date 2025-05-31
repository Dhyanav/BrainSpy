1.) How can we read and load NIfTI and DICOM files in Python ?

We use nibabel for .nii files and pydicom for .dcm files to load the data. For reading the data, .nii data is read as a 3d voxel array where as .dcm is read as individual slices (generally axial).

2.) What is the internal structure and metadata of these formats ?

-> .nii files are stored as 3d voxel array.
Image Shape: It is number of voxels in each dimensions
Affine Matrix: Let us assume a voxel. Its indices are vector, v = [i, j, k, 1].T . Affine matrix, A converts this vector into coordinates, u = Av. The 3*3 matrix in top-left corner represnts scaling, rotation, etc. While the fourth column serves as bias.
Voxel Spacing: It is the dimension of each voxel.
Data type: Data type stroed in voxel. Eg: int16, float64, etc.
Header fields: Some space is allotted to describe information regarding structure of file. Header file serve as kind of dictionary. Eg: header field 'data_type' indicates data type of the file.

-> .dcm files are stored as individual slices of scan, generally along axial direction.
We can extract meta_data like PatientID, etc using '.' operator.

3.) How do we stack DICOM slices into a 3D volume?

We read all slices, in accordance to their name. Eg: Slice 0 will be stored as "....Slice_000.dcm" and so on.
Then after we have collected all the slices in an array, we extract pixel data from each slice and store it in a 3d array.

(Following was done for ease of plotting data)
However, problem with this approach is that, if we want consistency with .nii data, we will have to move first axis to third axis.
THis is beacuse, in our stacked .dcm data, first axis corresponds to slice number.
But, in .nii data, third axis correspons to slice number.

4.) How can we visualize anatomical planes from a 3D image volume?

We create a function which takes 3 indices(along 3 principal axes) as input and just slice the 3d array according to that. Then, we plot the slice using matplotlib.

5.) Orientaion in .nii and .dcm

-> .nii
[ x y z 1 ].T   = [ R11  R12  R13  T1      *  [ i j k 1 ].T
                    R21  R22  R23  T2
                    R31  R32  R33  T3
                    0    0    0    1   ] 

R represents the part of matrix responsible for rotation. (similar to weights)
T represents the part of matrix responsible for translation. (similar to bias)

-> .dcm
There are various header tags which help us in this.
First, Patient Orientation: Two vectors describing directional cosines along row and columns. Lets call them r = [rx ry rz] and c = [cx cy cz]
Second, Pixel Spacing: They indicate dimension of each pixel. Lets call it [dx dy]
Third, Patient Position: It tells us coordinate of top-left pixel. Lets call it [x0 y0 z0]
Fourth, Slice Spacing: Spacing between consecutive slices. Lets call it dz

We define another quantity, directional cosines along spacing direction. It is cross product of r and c. Lets call it [sx sy sz]

Now, for any general voxel [i j k], coordinates [x y z] are given by
[x y z] = [x0 y0 z0] + i*dx*[rx ry rz] + j*dy*[cx cy cz] + k*dz*[sx sy sz]

6.) Differences between NIfTI and DICOM.
-> Usgae: NIfTI is used for research purposes and DICOM is used for clinical purposes.
-> Meta data structure: In NIfTI, meta data is 3d voxel array. In DICOM, meta data is 2d pixel array of each slice and each slice is stored seperately as a file.
-> File Formates: NIfTI only has one file while DICOM has individual files for all slices.
-> NIfTI is easier to use. DICOM is also easy to use, but it requires a bit more work.
