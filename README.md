### What is the problem?

##### Fresh Foods grocery chain stores is dealing with lot of issues related to theft of their stock. Stealing by employee to customer, item not getting scanned, manipulating price while scanning item by employee for a family/friend customer, scanning lower price item and this doesn't get caught until inventory review is done. These are issues related to inventory. There are various issues related to employees(cashier) : Reliable, hardworking employees are hard to find. 

### Solution: 

##### Solution for the issue with "just walk out technology". In this technology, when customer enters the store by scanning barcode(assuming customer is registered with fresh foods) , pick-up item and walk out of the store. This will solve the issues of employee and can prevent theft like item is not scanned, price manipulating and others mentioned above. 
##### Just walk out of technology involves image classificiation which is used to detect different objects(inventory), facial recognition(which is used for customer from entering to store to walking out of store)
##### Here I have used 2 objects(inventory items) : bottle and bar(figbar-cinnamon flavor). In order to train model to identify this objects I have used InceptionV3 and MobilenetV2 respectively.
##### For facial recognition, I have used opencv-python(cv2) for face capturing and matching face with captured is done with deepface model : sface.

### Data Source:

##### I have collected some images from google while I captured others at home. Initially I trained object using rented GPU at my local system. Back then I divided bottle images to 280images in train and 72 images in test. And for bar 324 images to train and 96 images to test. Each image was annoted with bounding box and class label. Later I created 3 datasets, 1 for bottle, 1 bar and 1 common for bar&bottle. The reason I created 3rd dataset is to verify that when bottle image is matched, it says label bottle and when bar image is matched it says bar. I divided this datasets into train, validation and test.

#### Data Preprocessing and cleaning:

##### Data cleaning and preprocessing are essential steps in preparing an image dataset for classification tasks. General outline of the process:
##### 1. Data Cleaning
##### 2. Data Inspection
##### 3. Negative object handling in image
##### 4. Resizing and Standardization
##### 5. Data Augmentation
##### 6. Data Splitting
##### 7. Annotating Data
##### 8. Data Loading 

### Pre-trained Model Comparison:

#### I have compared model faster-rcnn with inceptionV3 for bottle. InceptionV3 to MobileNetV2 for bar.  In faster_rcnn, the loss was not stable and at one point it felt like overfitting but there were many false positives than true positive and true negative. The visualization of faster_rcnn vs inceptionV3 captured from tensorboard are added to Visualization folder. When it comes to accuracy, faster_rcnn detect true positive with 51% while false negative with 98% wherease inception_v3 doesn't detect false positive and has accuracy for true positive  as 75%.
#### When comparing model inceptionV3 Vs MobileNetV2 for bar, the loss kept on increasing in inceptionV3 for bar so stopped training. the graph of loss is added to Visualization folder. The accuracy for mobilenet_v2 is 93% when trained with gpu.
#### Using pretrained model with transfer learning approach provides better accuracy, the project can be done in timely manner and it's less expensive than building model with scratch.


### Facial Recognition

#### For this technology, dataset would be the customer present in the store. Opencv-python is used to capture person's photo and pretrained library deepface is used to verify that face that the person entered the store photo same as the person picked up an item from rack. This face detection captures photo when customer is entered the store, picks up item and verify that face in a particular folder called "face" where all the customers entered the store captured faces are there. Verification is done on the basis of euclidian score, if the score is lowest for face captured, they are considered as best possible matches. There are various models like facenet, vgg, sface can be used with deepface for verificaiton, I chose sface specifically because in my testing with different combinations, it turns out sface can detect face when person with/without face painting, when person with/without glasses(including reading glass),when person with/without beard/mustache. 

### Next steps:

#### deploying this model of object detection with live capturing video technology where bar and bottle are detected live. Also I will be adding counting of objects so that can be used as inventory counting. Integrating face technology with live object detection counting and testing ; and testing whole piece at one for "just walk out technology".
