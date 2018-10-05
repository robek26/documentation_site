
---
layout : post
permalink : /chestx_documentation/

---

### Introduction

This project is focused on using AI to diagnose 14 potential diseases/abnormalities from a chest xray image and use a web application to make the AI be easily accessible for users. The diseases/abnormalities that are diagnosed are **Atelectasis,Cardiomegaly,Effusion	,Infiltration,Mass,Nodule,Pneumonia	,Pneumothorax	,Consolidation,Edema,Emphysema,Fibrosis,P.T.,Hernia**. The AI model used was regarded by many as being better at detecting the above diseases/abnormalities than radiologists. This claim is still debated by many AI developers and medical professionals.

### Libraries/Frameworks used to build the system

* **CheXNet Replica** An opensource DenseNet Model built by other developers using the model architecture from the original CheXNet authors.
* **Anaconda with python 3.6** Python Framework to build 
* **Keras** Library to build and train different kinds of Neural networks. The **CheXNet** model is built using this library.
* **ASP.NET with C# using MVC Architecture** Framework used to build the web application. Used Visual Studio 2017.
* **Dropbox Api** Library to download/upload images from/to dropbox.

### How the System Works

This application is built to work as an application that can be used in a medical facility. Let's look at the image below and explain how the system works.

![top level design](/{{site.baseurl}}/assets/images/top_level_design2_chestx.png) 

**Web Client:-** The web client is used to provide a user interface for users *(Medical Professionals)* to access patient information,register new patients and  upload chest x-ray images to server and get results back. The web client is written in C#.

**Database:-** The Database is used to store patient information and diagnosis history.

**Image Classifier Model:-** this model takes in an xray-image and outputs 14 diagnosis and the area on the image where the abnormalities are detected.

**Cloud Storage (Dropbox):-** Used to store images and later be accessed by the ML model or Web client.

### How the AI Model Works

![model](/{{site.baseurl}}/assets/images/model_chestx2.png)

The Model takes a chest x-ray image to predict if signs of any the 14 disease/abnormalities exist in the image. The model outputs a number that tells the probability of each disease. And to identify which area of the chest is infected, the system uses **class activation map(CAM)**. CAM is used to make the model to display the area of the image that led it to decide a certain abnormality is present. After prediction is complete the proabilities are stored in database and the cam images are uploaded to dropbox with their access url stored in the patient database.

### How To Use The Application

Before launching the web application, the server that runs the model must be launched. Then we launch the web app.

![use1](/{{site.baseurl}}/assets/images/chestx_img_1.png)

Consider this application is used in a medical center. The First page of the application shows complete patient list. The list is paginated so only 10 patient information is displayed. The page has a search and sort functionality to located patients easily. The user can register new patient,edit and see detailed information about a patient easily.

![use2](/{{site.baseurl}}/assets/images/chestx_img_2.png)

User can register a new patient buy filling the form above.

![use3](/{{site.baseurl}}/assets/images/chestx_img_3.png)

Existing patient information can be edited using the form above.

![use4](/{{site.baseurl}}/assets/images/chestx_img_4.png)

On the patient lists in the first page, the user can click on `Details` button next to specific patient's row and open the detail page as shown above. The page contains patient information and all the x-ray images taken from this particular patient. The `Upload New Xray` button opens a page to upload a new xray image to the server and get it processed. The user can click on the images to see a detailed diagnosis result.

![use4](/{{site.baseurl}}/assets/images/chestx_img_5.png)

The user can upload new image from the page shown above.

![use4](/{{site.baseurl}}/assets/images/chestx_img_6.png)

After an image is uploaded, it takes few minutes to process the image so the modal box is shown to the user to be patient for a few minutes.

![use4](/{{site.baseurl}}/assets/images/chestx_img_7.jpg)

After processing is complete, the above page will be displayed to show the results to the user. 










  