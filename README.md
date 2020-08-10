# SIIM-ISIC-Melanoma-Classification

![](https://github.com/CodingWitcher/SIIM-ISIC-Melanoma-Classification/blob/master/images_for_readme/rbc.webp)

# (I) Abstract : 

Skin cancer is the most prevalent type of cancer. Melanoma, specifically, is responsible for 75% of skin cancer deaths, despite being the least common skin cancer. In this project we aim to analyze and identify melanoma in lesion images. Current disease diagnosis based on human labor is not only time-consuming but may prove to be inefficient as well. This endeavor of ours aims to leverage the potential of **Computer Vision** and **Machine Learning** to *to successfully categorize the given melanoma image into malignant or benign*. 

Melanoma is a deadly disease, but if caught early, most melanomas can be cured with minor surgery. Image analysis tools that automate the diagnosis of melanoma will improve dermatologists' diagnostic accuracy. Better detection of melanoma has the opportunity to positively impact millions of people.

This project was a part of '**SIIM-ISIC Melanoma Classification**' challenge hosted on Kaggle.

Read more at : **https://www.kaggle.com/c/siim-isic-melanoma-classification** 

# (II) Dataset Used : 

The dataset was generated by the *International Skin Imaging Collaboration (ISIC)* and images are from the following sources: *Hospital Clínic de Barcelona, Medical University of Vienna, Memorial Sloan Kettering Cancer Center, Melanoma Institute Australia, The University of Queensland, and the University of Athens Medical School*. A copy of the dataset was made available on Kaggle platform and may also be located on *ISIC 2020* challenge webpage. The links are pasted below : 

* **The ISIC 2020 Challenge Dataset :** **https://challenge2020.isic-archive.com/**
* **Kaggle :** **https://www.kaggle.com/c/siim-isic-melanoma-classification/data**

The dataset was made available under *Creative Commons Attribution-Non Commercial 4.0 International License*.

It encapsulated : 
* Images in **DICOM**, **jpeg** and **TFRecord** format.
* 33,126 training images were provided along with 10,982 test images.
* Each image belonged to either of the two categories : **malignant** or **benign**.

Some randomly sampled images from the training set : 

![](https://github.com/CodingWitcher/SIIM-ISIC-Melanoma-Classification/blob/master/images_for_readme/melanoma_sample_01.jpg)
![](https://github.com/CodingWitcher/SIIM-ISIC-Melanoma-Classification/blob/master/images_for_readme/melanoma_sample_02.jpg)
![](https://github.com/CodingWitcher/SIIM-ISIC-Melanoma-Classification/blob/master/images_for_readme/melanoma_sample_03.jpg)


# (III) Libraries Used : 

* **Numpy** : Fundamental package for scientific computing in Python3, helping us in creating and managing n-dimensional tensors. A vector can be regarded as a 1-D tensor, matrix as 2-D, and so on.

![](https://raw.githubusercontent.com/CodingWitcher/Leaf_Diseases/master/images_for_readme/tensor.jpg)

* **Pandas** : Pandas is a software library written for the Python programming language for data manipulation and analysis. In particular, it offers data structures and operations for manipulating numerical tables and time series.

![](https://github.com/CodingWitcher/SIIM-ISIC-Melanoma-Classification/blob/master/images_for_readme/pandas.jpeg)

* **Matplotlib and Seaborn** : Python3 plotting libraries used for data visualization.

![](https://github.com/CodingWitcher/SIIM-ISIC-Melanoma-Classification/blob/master/images_for_readme/data%20viz.png)

* **OpenCV** : OpenCV (Open Source Computer Vision Library) is an open source computer vision and machine learning software library. OpenCV was built to provide a common infrastructure for computer vision applications and to accelerate the use of machine perception in the commercial products. The library has more than 2500 optimized algorithms, which includes a comprehensive set of both classic and state-of-the-art computer vision and machine learning algorithms. The library is used extensively in companies, research groups and by governmental bodies.

*Homepage* : **https://opencv.org/**

![](https://github.com/CodingWitcher/SIIM-ISIC-Melanoma-Classification/blob/master/images_for_readme/pyopencv.png)

* **Tensorflow** : Is an open source deep learning framework for dataflow and differentiable programming. It’s created and maintained by Google.

![](https://github.com/CodingWitcher/SIIM-ISIC-Melanoma-Classification/blob/master/images_for_readme/tensorflow.png)

* **SciKit-Learn** : Scikit-learn is a free software machine learning library for the Python programming language. It features various classification, regression and clustering algorithms. 

![](https://github.com/CodingWitcher/SIIM-ISIC-Melanoma-Classification/blob/master/images_for_readme/sklearn.webp)

* **tqdm** : Is a progress bar library with good support for nested loops and Jupyter notebooks.

# (IV) Accelerator Initialization and Dataset Loading Using tf.data API: 

For this project we worked using **TFRecords**, which is binary storage format for our data. 

## Advantage of Binary Storage Scheme of TFRecords : 

![](https://github.com/CodingWitcher/SIIM-ISIC-Melanoma-Classification/blob/master/images_for_readme/tfrecords.png)

The binary storage data takes up relatively low space on our disk, and hence it takes less time to copy and can be read much more efficiently! Moreover, the tensorflow framework is optimized to handle tfrecords amazingly well.

The datasets that are too large to be stored fully in memory, this is an advantage as only the data that is required at the time (e.g. a batch) is loaded from disk and then processed.

Another major advantage of TFRecords is that it is possible to store sequence data — for instance, a time series or word encodings — in a way that allows for very efficient and (from a coding perspective) convenient import of this type of data.

## TFRecord :

A TFRecord file contains an array of **Examples**. *Example is a data structure for representing a record*, like an observation in a training or test dataset. A record is represented as a set of **features**, each of which has a name and can be an array of bytes, floats, or 64-bit integers.

To summarize:

* **An Example contains Features**.
* **Features is a mapping from the feature names stored as strings to Features**.

These relations are defined in *example.proto and feature.proto* in the TensorFlow's source code, along with extensive comments. As the extension *.proto* suggests, these definitions are based on protocol buffers.

## So, What are Protocol Buffers ? 

![](https://github.com/CodingWitcher/SIIM-ISIC-Melanoma-Classification/blob/master/images_for_readme/protocol%20buffers.png)

Google’s Protocol buffers are a serialization scheme for structured data. In other words, protocol buffers are used for serializing structured data into a byte array, so that they can be sent over the network or stored as a file. In this sense, it is similar to JSON, XML.

**Protocol buffers can offer a lot faster processing speed compared to text-based formats like JSON or XML**.

The aforemntioned TFRecords are crunched using **TPU** which we initialized in our code.

## Tensor Processing Unit(TPU) :

TPUs are hardware accelerators specialized in deep learning tasks. We used the one provided by Kaggle platform for this project. 

![](https://github.com/CodingWitcher/SIIM-ISIC-Melanoma-Classification/blob/master/images_for_readme/tpu_cores_and_chips.png)

Each TPU core has a traditional vector processing part (VPU) as well as dedicated matrix multiplication hardware capable of processing 128x128 matrices. This is the part that specifically accelerates machine learning workloads.

TPUs are equipped with 128GB of high-speed memory allowing larger batches, larger models and also larger training inputs.

## Dataset loaded using tf.data API : 

The tf.data API enables us to build complex input pipelines from simple, reusable pieces and use the resources to a superlative degree of efficiency. Hence, these effective data pipelines ensures that our accelerator TPU/GPU is always crunching and stays idle for a minimum time span.

The following will illustrate the advantage of an efficient pipeline design : 

![](https://github.com/CodingWitcher/SIIM-ISIC-Melanoma-Classification/blob/master/images_for_readme/pipelining.png)

# (V) 
