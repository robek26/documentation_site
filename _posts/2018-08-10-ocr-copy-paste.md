---
layout : post
permalink : /ocr_copy_paste/

---

### Introduction

OCR (optical character recognition) is the recognition of printed or written text characters by a computer. This involves photoscanning of the text character-by-character, analysis of the scanned-in image, and then translation of the character image into character codes, such as ASCII, commonly used in data processing.

This project is focused on extracting a text from a screen and paste it in any text editor.

### What i used to build the system

* Screen Snipper tool written in **java**
* **Anaconda** with python 3.5.3
* External python libraries
    * **pytesseract** text from image extractor.


### How The System Works

![top level design](/{{site.baseurl}}/assets/images/ocr_img0.png)

When the application user wants to extract text from a screen like codes on youtube tutorial videos, texts that can't be copied using the usual copy/paste routine etc., First the `screen snipper` module will snip the selected part and convert it to an image. The image is sent to the ocr server for processing. When the `Server` receives a new image, it sends it to the `OCR Engine` and the engine tries to extract the text. If the extraction is successfull, the extracted text will be sent back to the client and put in a `clipboard`. The user can then be able to paste the text to any editor.

### How To Use The Application

A user is wathcing a youtube tutorial about c++ programming and wants to copy the code in the video.

![Img 1](/{{site.baseurl}}/assets/images/ocr_img1.png)

On the menu bar, click on the yellow box icon and a popup menu will appear showing `Snip Screen` option. Click on it and the whole screen dims.

![Img 2](/{{site.baseurl}}/assets/images/ocr_img2.png)

After the screen dims, select the part of the text to extract.

![Img 3](/{{site.baseurl}}/assets/images/ocr_img3.png)

After Selection, the application will send the selected image to the processor and waits for a response. As you can see on the image above, we have a notification saying the Text is copied to clipboard. After few seconds the notification disappears.

![Img 4](/{{site.baseurl}}/assets/images/ocr_img4.png)

Open a text editor and paste the text in the clipboard.

![Img 5](/{{site.baseurl}}/assets/images/ocr_img5.png)

### How to Launch The Application

1. Go to the directory where the source code is kept.
2. Activate anaconda environment `source activate <ENV NAME>`.
3. To launch the server, run `ocr_server.py` file.
4. To launch the client, run `TextCopier.java` file.


### Demo

{%  include youtubeplayer_ocr.html %}




**You can find the source code of this project [here.](https://github.com/robek26/ocr_copy_paste){:target="_blank"}** 




