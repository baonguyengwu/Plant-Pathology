README
 
 
 	 
 
Executive Summary
The purpose of our application is to increase the efficiency in which disease diagnosis is being completed.  Specifically, we will focus on the apple tree and two of the most prevalent diseases affecting that tree; apple rust and apple scab.  The primary way of disease diagnosis is based on human scouting, which can be time-consuming and expensive. Some computer-vision-based models should increase efficiency; unfortunately, because of the significant variance in symptoms due to the age of infected tissues, genetic variations, and light conditions within trees, the accuracy and detection of these models can be significantly compromised. With the improved accuracy of our program, farms can more quickly and, with lower costs, decide what treatment options to use. 
Pathogen identification is a redundant, expensive, and inefficient task when done by the human eye.  Once a model is adequately trained, this task could be performed not only much more accurately but much more efficiently as well.  

 
Data Description
This dataset is a part of Kaggle's Plant Pathology 2021 – FGVC8 code challenge. The data consists of train.csv (training set metadata), test.csv (sample submission file in the correct format), train_images (training set images), test_images (the test set pictures). Within train.csv and test.csv, there are two primary columns: image (the image ID) and labels (the target classes, a space-delimited list of all diseases found in the picture). The dataset also consists of 18000 high-quality RGB images of apple foliar diseases, including a sizeable expert-annotated disease dataset. The total size of the data is approximately 15 gigabytes. However, this is pretty challenging to process due to the limitations of the accessible version of Google Colab. We will have to figure out qa way to utilize the Google Colab result without decreasing the quality. We will consider an option to reduce the file size. Doing so will result in a decrease in the accuracy of the model. We can still utilize some other techniques like image rotation, drop out, and VGG16 alongside the CNN model to increase the accuracy. 
 
Research Questions 
	The main objectives of our project are to accomplish the specific goals of the Fine-Grained Visual Categorization (FGVC8) workshop at the CVPR2021, where it asks developers to develop machine learning-based models to: 
-	Accurately classify a given leaf image from the test dataset to a particular disease category.
-	Identify an individual disease from multiple disease symptoms on a single leaf image.
-	Deal with rare classes and novel symptoms
-	Address depth perception—angle, light, shade, and age of the leaf
-	Incorporate knowledge in identification, annotation, quantification, and guiding computer vision to search for relevant features during learning.
According to Reuters, the spread of pests and pathogens that damage plant life could cost global agriculture $540 billion a year (Stock 2017). The report, released by the Royal Botanic Gardens (RBG) at Kew in London, stated that an increase in international trade and travel had left flora facing rising threats from invasive pests and pathogens for more significant biosecurity measures. Current disease diagnosis based on human scouting is expensive and too time-consuming. This could be a massive opportunity for our application to detect leaf diseases, especially for Apple Trees. A large orchard farm will lose a significant amount of revenue when the outbreak of apple trees happens. On the other hand, with smaller orchards, a loss in revenue might eliminate the business. With the increase in prediction accuracy, we can support large and small orchards to detect and prevent the outbreak of apple tree diseases. 
 
Methodology
First, we have to load the data into the environment. We decided to use the "pip install kaggle" and the Kaggle API to load the data directly into Google Colab. Doing so will bypass the 15 gigabytes limitation of the Googe Drive and load the data directly into the Google Colab, which provides us 50GB disk space and 12GB RAM for free. 
 
As in the screenshot above, a kaggle.json API key was uploaded to utilize Kaggle's API. 
 
Then, the dataset was downloaded and unzipped. This approach will faster than download the dataset from Kaggle, upload to Google Drive, and unzip it. Besides, since Google Drive's limitation is 15GB, the Kaggle API solves these limitations. 
After uploading and unzipping the data, we decided to draw a count plot to understand what's inside the dataset. The categories that have the most pictures are healthy and scab. 
 
To have more visualization into the data, we built a small function to display all the symptoms alongside the images: 
 
	For multi-label problems, we use binary cross-entropy. An image may have multiple labels. We need the probabilities that each of these labels corresponds to the given image; this can be considered as n independent binary classifiers for the n labels.		
	To achieve better accuracy, we decide to use the CNN model. Before using the CNN, there has to be some data prep beforehand. The image size is enormous; therefore, it took a little longer to run the CNN model. The images were split into a training set and a testing set as 8:2 ratio. The training set was used to build the model, and the testing set was used to validate the model's accuracy model. 
	The CNN model itself was built with multiple layers. There are numerous convolution and pooling layers for feature extraction. After some trials and errors, we noticed that putting three convolution and pulling layers yielded the best result. Even though splitting the data into an 8:2 ratio will reduce overfitting, we still need to address it by adding the Drop Out layer. Last but not least, we will place a sigmoid activation to provide relative probabilities of the training images being in any of the following four classes: "healthy," "multiple diseases," or "scab," or "rust."
Besides adding the Drop Out layer, we will also utilize the VGG16 pre-trained object recognition model to apply to the model to see if it will increase the training accuracy of the model. 
	After getting the model's accuracy, we will use the matplotlib library to draw some charts to help us visualize the model's accuracy. 
 
 
First model
 

The second model with VGG16 added
Result
	
Since it took so long for the model to run, we only used ten epochs. The accuracy will be increased if we choose a higher epoch, but since the time was slow, we kept the epochs at 10. The accuracy of the model is around 0.83. 






Adding VGG16 to the model does not make much difference since the epochs were still 10. 
 
We also add to the code the ability to use the model to predict any images. We upload the image to the Colab's runtime, load the image into Colab, and pass that image through our VGG16 classification model, and the result we get is healthy with 100% confidence. 
 
Conclusion
We successfully built a CNN Model with an accuracy of approximately 83%.  We utilized what we learn during the course (making a CNN, image processing, using VGG16 & Dropout) and applied that to the project. We believed with more epochs and processing power; we can increase the accuracy of the model. The goal of future enhancement could be to allow the user to upload the images, and then the program will return the result along with the accuracy. 
 
References
Stock, Matthew. “Pests and Pathogens Could Cost Agriculture Billions: Report.” Reuters, Thomson Reuters, 18 May 2017, www.reuters.com/article/us-environment-plants-idUSKCN18E005.


