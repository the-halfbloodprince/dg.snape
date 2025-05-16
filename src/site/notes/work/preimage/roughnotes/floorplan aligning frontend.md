---
{"dg-publish":true,"permalink":"/work/preimage/roughnotes/floorplan-aligning-frontend/","noteIcon":""}
---

#### Video Notes from Siddharth's video
2 steps:
- aligning the floorplans to each other
- using the aligned floorplans to match points on the density image which is generated during the processing steps
	- need a way to upload those images to s3 and fetch them as needed

Prototype:
- npm start
- ![Pasted image 20250128023259.png](/img/user/work/preimage/roughnotes/Pasted%20image%2020250128023259.png)
- Rotate Camera etc.
	- ![Pasted image 20250128023401.png](/img/user/work/preimage/roughnotes/Pasted%20image%2020250128023401.png)
- Multiple layers
	- ![Pasted image 20250128023437.png](/img/user/work/preimage/roughnotes/Pasted%20image%2020250128023437.png)
- we'll have elevations of every single floor on the floorplan
- change opacity of images (floorplans)
- add rotations, translations etc to the floorplans to align the floorplans to one another using say, common points available to us
- eg the top left pt of each floor plan can be aligned to each other so that they are on the same coordinate system
- ![Pasted image 20250128023853.png](/img/user/work/preimage/roughnotes/Pasted%20image%2020250128023853.png)
- select the relevant part
	- ![Pasted image 20250128023923.png](/img/user/work/preimage/roughnotes/Pasted%20image%2020250128023923.png)
	- select relevant parts on density images
		- ![Pasted image 20250128024002.png](/img/user/work/preimage/roughnotes/Pasted%20image%2020250128024002.png)
- mark points in both views
	- ![Pasted image 20250128024043.png](/img/user/work/preimage/roughnotes/Pasted%20image%2020250128024043.png)
- we get the overlaid image
	- ![Pasted image 20250128024212.png](/img/user/work/preimage/roughnotes/Pasted%20image%2020250128024212.png)
- 