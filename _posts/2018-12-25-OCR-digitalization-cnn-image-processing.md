---
title: Meta Tag Extraction
tags: [OCR, digitalization, cnn, image processing]
style: fill
color: dark
description: Glimpse of the journey exploring Image Processing and Documents.
---

<!-- Start Writing Below in Markdown -->

##### _Disclamier:_

This post is just a reflection of solving digitalization problem and starting line for such initivative. I have tried to ink the efforts and activities that took place in the developement of a Document Intelligance System. Most of the story told below has been replaced by many cool stuff and hacks while productizing the solution. Copyright issues and Funny Fear have stopped me including it into the post. :)

### Why this post?

Character Recognition is one of the unsolved problems present till date. Claims to solve it has been done in past but not to an extend that we can say `Ohh! my God, now no more resreach on it.` I also have tried to solve this problem and partially achieved it. Looknig at the future of this problem statement, I'm sure that many more brillinat minds are yet to come, take this problem and get more close to say it done. In order to do so I strongly feel thats it's better to start from a point where people have left so that we can invest our energy in going ahead instead of reinventing the wheel.

### Sounds Great, How does it started?

When I was working on a product Intelligent Automation Platform (IAP), we have a use case where clients need to extract information from thr documents. The usecase was huge as it converges to digitalization of all paper documents at a higher level. So in process of converting documents to searchable texts we developed Optical Character Recognition (OCR) system. The OCR would take the document and extract information from it.

### How was the journey?

The first problem with this usecase was the document quality. The document's qyality ranges for one end where we, as humans can’t read it to the other end whrere we have {fileName}.docx converted to pdf. We tried different algorithms to understand at what extend we can clean the images, before we go deep to identify/predict the **insiders**.

### Sorry you said _different algorithms_. Can you elaborate?

Please mention the stage wise approach and techinall difficulties.

Yeah Sure,

So We have images and the output demanded was the text it containes. As mentioned earlier the images can be very noise (thanks to the old printers). In order to run any prediction algorithm or tools over it, the must was to get rid of the noise it contains. The noise could also be in the form of attestation marks, signatures, curled marks on paper and many more abnormalities. We pass the document from two process. Denoising followed by binarization of the image.

- Denoising

  The denoisng process could be done by applying diffent menthods. One promising method was using machine learning to predict the noise and subcract it form the image(either Gloablly or Locally). In order to apply machine learing we need to have both the clean images and the noisy images. We acheived it by using clean images and applying diffrent layers of noise over it. For adding noise we did masking images, gaussian noise in which we change the value of the pixel by a small amount where the small amount is a value obtained from gaussian distribution, salt pepper noise where we do black and white some pixels randomly or as per some algorithms. The best results were of Ostu binarization(For binarization, will discuss after few linens) and Xgboost Algorithm.

- Binarization

  The binarization method could be a local or global one. As for global binarization we tried fixed threshold binarization adn for histogram based Otsu Binarization. For local binarizatin, we tried adaptive binarization, Niblack, Sauvola method. We also gave a shot to linear regression model. We trained the model by taking good quality image as output and added noise into to get a dirty image to train for. For adding noise we did masking images, gaussian noise in which we change the value of the pixel by a small amount where the small amount is a value obtained from gaussian distribution, salt pepper noise where we do black and white some pixels randomly or as per some algorithms.

Luckly OpenCv provides one of the popular algorithm for denoising as an inubild process `cv2.fastNlMeansDenoisingColored()`. We used cv2.fastNlMeansDenoisingColored() function which is the implementation of Non-local Means Denoising algorithm. Non-Local Denoising is based on a simple principle: replacing the color of a pixel with an average of the colors of similar pixels to denoise. Denoising is then done by computing the average color of these most resembling pixels. The resemblance is evaluated by comparing a whole window around each pixel, and not just the color. This new filter is called non-local means.

So We converted the images into grayscale first then get binarized images from them. Before binarization we also tried to denoise the image using opencv inbuild functions.

### What's next?

Once the image is denoisesd and converted into binary values, The main task is now to predict the character. For this tessetact-4 was an awesome choice as it has an LSTM mode, normal mode and an option to use both. One problem with this method was that it can not be trained on limited dataset. What I meann is that if we want it to train only on numbers it isn't possible. So for region where we have to extract only numbers this model doesn’t put impressive results. So we trained cNN model for that.

### Wait from where you get the dataset?

The dataset was available from internet as EMNIST dataset, Char74k, and many images that we created of our own. We trained the model over the given images.

### What about the AI part?

The CNN architecture was inspired by LeNet5. Changing the default structure and ensemble with data argumentation was a good approach. But that didn't helped much. Also as the data wasn't huge enough, posibilities of overfitting was always there. This possibility stoped us making it more fansty and huge. The backend was deployed in as python REST API. When the folder path is provided to the API the process stores the result into the database. As soon as the database is populated with the result it is reflected back to the user.

# Can you give us some referecne for the above claim ?

Sure but Can I include Wikipedia (Ahea! that not a source, but anyway we will have a look ;( )
https://en.wikipedia.org/wiki/Image_noise
NonLocal: http://www.ipol.im/pub/art/2011/bcm_nlm/article.pdf

https://en.wikipedia.org/wiki/Thresholding_(image_processing)
Different Binarization:
https://www.irjet.net/archives/V3/i3/IRJET-V3I3241.pdf
Theise: http://cgi.di.uoa.gr/~phdsbook/files/Ntirogiannis%20Kostas.pdf

https://pdfs.semanticscholar.org/c58f/8ab48711f0d5596be78c7f403027030ecc5b.pdf

https://www.ijsr.net/archive/v4i11/NOV151039.pdf

https://www.irjet.net/archives/V3/i3/IRJET-V3I3241.pdf

https://en.wikipedia.org/wiki/Otsu%27s_method

http://biomedpharmajournal.org/vol7no2/image-sharpening-by-gaussian-and-butterworth-high-pass-filter/

https://medium.freecodecamp.org/getting-started-with-tesseract-part-ii-f7f9a0899b3f

https://medium.freecodecamp.org/tagged/tesseract