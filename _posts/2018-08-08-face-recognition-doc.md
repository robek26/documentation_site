---
layout : post
permalink : /actor_rec/
---


### Introduction

A facial recognition system is a technology capable of identifying or verifying a person from a digital image or a video frame from a video source. There are multiple methods in which facial recognition systems work, but in general, they work by comparing selected facial features from given image with faces within a database.

This project is focused on extracting an actors face from a movie, identify their name using facial recognition algorithm and open their imdb page to view their biography and other movies they have worked on.

### What i used to build the system

* Screen Snipper tool written in **java**
* **Anaconda** with python 3.5.3
* External python libraries
    * **face_recognition** simple face encoder and recognizer built on top of **dlib** library.


### How The System Works

![top level design](/{{site.baseurl}}/assets/images/face_rec_toplevel_2.png)

When a person is watching a movie and suddenly sees an actor/actress that is interesting and wants to find out more about them, he will pause the movie and use the the screen snipper tool to snip the face of the actor. The `screen snipper` module shown in the above image does this. After the image is taken the `sender receiver` module will send the image to server that processes the image. The `screen snipper` and `sender receiver` module are written in java.

On the `server` side, the image will be received and forwarded to `face detector` module. The `face detector` module makes sure there is a person's face in the image. If there is no face, it will send an error message back to the server and the server forwards the message to the image sender. If the image has a face in it, the `face detector` encodes the face to a 128 length number array and send it to the `face recognizer` module. The `face recognizer` module will compare the encoded face to a database of 1000 actors/actresses to find a close match and sends back a response to the `server`. The `server` then sends the message to the client. The `server`,`face detector` and `face recognizer` modules are written in python.

The response message contains either a **Face not recognized** message or json string with **actor name and imdb url**. Once the client application receives the response text from the server, depending on the response it either displays the error message or launches a web browser and loads the actor's imdb page.

### How was the face database built?

To build the database for the 1000 actors and actresses, i followed three steps.

#### Step 1. Getting the 1000 actors names

![step 1](/{{site.baseurl}}/assets/images/facerec_step_1.png)

As you can see in the above image, there is an imdb top 1000 actors page. Actually it is a 10 page list. So i wrote a small scraper in python to extract all the names and imdb_id (nmxxxxxx) and put it in a sqlite database. 

#### Step 2. Downloading Images of Each Actor

![step 2](/{{site.baseurl}}/assets/images/facerec_step_2_1.png)

Here on step 2, we have an image grabber script that connects to dogpile search engine, scrapes image urls and  downloads images(30) of each actor using the actors name list. The downloaded images are kept in a local directory for further processing.

#### Step 3. Encoding the Face Image of Each Actor

![step 3](/{{site.baseurl}}/assets/images/facerec_step_3.png)

Once we have all the images necessary, Each image is sent to `face detector` module to check if there is a face in the image and the `face encoder` module encodes the images and store them in a database. As stated in step 2 we have 30 images of each actor but only 10 are encoded. This is done to make sure if an actor has few images where their face can't be detected, then there will be uneven number of face encodings for each actors. So to make the process easier we have 30 images of each actor and encode 10 of them.


### How To Use The Application

![Img 1](/{{site.baseurl}}/assets/images/fr_img5.png)

On the menu bar, click on the smiley face icon and a popup menu will appear showing `Snip Screen` option. Click on it and the whole screen dims.

![Img 2](/{{site.baseurl}}/assets/images/fr_img6.png)

After the screen dims, select the face of the actor to identify .

![Img 3](/{{site.baseurl}}/assets/images/fr_img7.png)

After Selection, the application will send the selected image to the processor and waits for a response. As you can see on the image above, we have a notification saying the face is recognized and whose face it is. After few seconds the notification disappears.

![Img 4](/{{site.baseurl}}/assets/images/fr_img8.png)

While the notification is displaying, the browser will open and load the imdb page of the identified actor.

**N.B.** The system sometimes makes mistake of misidentfying actors as you can see in the demo video. But the good thing is the misidentied actors closely resemble the selected actors in the movie.


### How to Launch The Application

1. Go to the directory where the source code is kept.
2. Activate anaconda environment `source activate <ENV NAME>`.
3. To launch the server, run `facerec_server.py` file.
4. To launch the client, run `SystemTrayProg.java` file.


### Demo

{%  include youtubeplayer_facerec.html %}




**You can find the source code of this project [here.](https://github.com/robek26/ActorRecognizer){:target="_blank"}** 
    

