# Notice
This folder contains three main folders: CurveFaultA, CureveVelA, FlatFaultA.
These three datasets are all from OpenFWI (data download: https://smileunc.github.io/projects/openfwi/datasets)
Except for CurveVelA, there are 108 velocity model .npy files in each folder.
In addition, there are 500 velocity models within each .npy file.

Currently, training and testing velocity models (vmodelX.npy) for all data have been provided, but seismic records (seismicX.npy).
However, seismic records (seismicX.npy), velocity model contours (cvmodelX.npy), and low-resolution reconstructed velocity models (lvmodelX.npy) need to be generated by the user.

---

**1.Seismic records are the basis for any network training.**  
It will be forward generated through "forward2openfwi.py" in the root directory (Note! This process is very time-consuming).

**2.Velocity model contours are the basis for DDNet70 and DenseInvNet training.**  
It will be generated by "create_contour_vmodel.py" in the current directory.

**3.The low-resolution reconstruction velocity model is key to DenseInvNet training.**  
It requires users to generate it through their own trained LResInvNet network or the network we have provided in the models folder.  
Specifically, the user is required to select the command in the test file: "-n {} -net LResInvNet -bv -nep .\models\{}Model\LResInvNet_100of100.pkl".  
Meanwhile, the user needs to set multi_or_single to 0 and execute the function temp_tester.save_lowres_inversion_results().  
In this way, the low-resolution velocity model output by LResInvNet will be automatically saved in the corresponding dataset in the data folder.  

Complete folder example:  
|data  
|===CurveFaultA  
|=====cvmodel1.npy  
|=====cvmodel2.npy  
|=====...  
|=====cvmodel108.npy  
|=====lvmodel1.npy  
|=====lvmodel2.npy  
|=====...  
|=====lvmodel108.npy  
|=====seismic1.npy  
|=====seismic2.npy  
|=====...  
|=====seismic108.npy  
|=====vmodel1.npy  
|=====vmodel2.npy  
|=====...  
|=====vmodel108.npy  
|===CurveVelA  
|===FlatFaultA  
|===create_contour_vmodel.py  
|===create_dir_txt.py  

---

Finally, the configuration folder records the arrangement of the training and test sets.
"_base" represents the configuration files of InversionNet and VelocityGAN.
"_cont" represents the configuration file of DDNet70.
"_lres" represents the configuration files of LResInvNet and DenseInvNet.

---

When all the data is ready, the size of the data folder may reach 259G, so please pay attention to the hard disk space allocation.



