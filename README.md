Team Name: VU
Team Memebers: Mahmoud Mousatat , Made Oka Resia Wedamerta
Solution Overview:

Our solution is primarily focused on determining the velocity and accurate distance of a specific location and subsequently using a depth map to reference all other objects. We began by training the YOLOv8 model, a principal object detection framework, on a training dataset. This model was rigorously trained to recognize key objects in a test dataset. We utilized approximately 90,000 images, derived from video footage and annotated with bounding boxes, for a single training epoch. The entire process of preprocessing the training dataset and the training itself is projected to take around 2 hours on an A100 GPU, with a batch size limited to 4 due to memory constraints encountered at a size of 8. However, the limited variety in our dataset presented challenges in accurately detecting objects at varying distances, a key issue that affected the reliability of our distance calculations based on velocity vectors and previous estimates.

Upon successfully training YOLOv8, we leveraged MiDaS v3 to generate depth maps. By approximating the distance to the nearest ground point using average human height and camera angle, we were able to determine the actual distance to this point. The depth map then facilitated the estimation of the real distance to objects of interest, scaled appropriately.

The final step involved calculating the velocity. This was done by averaging the distance covered by a person during their walk and then treating this average as a constant velocity (assuming uniform speed). While this approach is adaptable to varying speeds, it requires more extensive data for accurate application.

Potential Improvements:

Enhancing Distance Estimation: We aim to refine object distance estimation by integrating a neural network trained on the KITTI Dataset. This addition would enable distance calculations based on bounding boxes, images, and object detection. Although preliminary tests with this model showed promising results, we opted to defer its implementation for more complex samples, as our current velocity calculations are based on the assumption of straight-line movement at a nearly constant speed. This assumption is supported by the stability in the size and position of bounding boxes.
Limitations and Their Causes:

Lack of Ground Truth Data: The absence of ground truth distance data in the training set led to less precise speed estimations. We managed to calculate an estimated speed based on the average distance from detected objects in the test dataset. To compensate for this limitation, we introduced a correction factor 'X', which could be more accurately determined using additional measurement tools such as accelerometers or gyroscopes in the training dataset. This factor would then be uniformly applicable across both training and testing datasets.
