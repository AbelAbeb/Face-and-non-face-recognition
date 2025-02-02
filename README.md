# Face and Non-Face Recognition

## Table of Contents
1. Introduction
2. Getting Started
3. Usage
4. Contributing
5. License

## Introduction
This project is a machine learning model for face and non-face recognition. It uses various techniques such as Principal Component Analysis (PCA), Linear Discriminant Analysis (LDA), and different classifiers to distinguish between images of faces and non-faces.

## PCA
Principal Component Analysis (PCA) is a dimensionality reduction technique that is used to extract important features from high-dimensional datasets. PCA works by identifying the principal components of the data, which are linear combinations of the original features that capture the most variation in the data

LDA
Linear Discriminant Analysis (LDA) is a dimensionality reduction technique that is used to reduce the number of features in a dataset while maintaining the class separability. LDA is a supervised technique, meaning that it uses the class labels to perform the dimensionality reduction. LDA is a popular technique for dimensionality reduction in the field of pattern recognition and machine learning

## Dataset
+ The dataset for this project is the AT&T Face Database
- The dataset is open-source and can be downloaded from Kaggle.
* The dataset contains 400 images of 40 people, each person has 10 images.
+ The images are of size 92x112 pixels & in grayscale.
+ The Data Matrix is 400 x 10304 where each image is flattened in a vector and saved as a row in the Matrix
  
## Getting Started

### Prerequisites
Before you begin, ensure you have met the following requirements:
- You have installed the latest version of Python.
  ~~~ paython
  python 3.xx
  ~~~
- You have a basic understanding of machine learning concepts.
- You have the necessary Python libraries installed.
- These include `os`, `numpy`, `matplotlib`, `seaborn`, `PIL`, `sklearn`.

### Implementation 
#### **Libraries Used**
- NumPy
* Scikit-learn
+ Images

### Data Preprocessing

#### Face Images and Non-Face Images
1. Download a semi large dataset of non faces images (~550) sample.
2. Loaded non-face images from the specified file paths.
3. Convert images into gray scale
4. Resized each image to 92x112 pixels.
5. Flattened each image to a 1D array.
~~~ python
def load_images(path):
    images = []
    labels = []
    if path:
        for i, dir in enumerate(os.listdir(path)):
            for file in os.listdir(os.path.join(path, dir)):
                img = Image.open(os.path.join(path, dir, file)).convert('L')
                img = img.resize((92,112))
                images.append(np.array(img).flatten())
                labels.append(i+1)

    return np.array(images), np.array(labels).reshape(-1,1)
faces, labels = load_images('/content/drive/MyDrive/ColabNotebooks/ML_project_classification/datasets/faces')
non_faces, non_labels = load_images('/content/drive/MyDrive/ColabNotebooks/ML_project_classification/datasets/nonfaces')

~~~
#### Labels
1. Created binary labels (1 for faces, 0 for non-faces).
  ~~~ python
      print(faces_labels[99])
  ~~~

#### Shuffle images within each class
why shuffling is basically use to be sure that you don't have bias when you spliting data into training and testing 
1. shuffle face images and thier labels
2. shuffle non_faces images and thier labels
~~~ python
def shuffle_data(data, labels):
    idx = np.arange(data.shape[0])
    np.random.shuffle(idx)
    return data[idx], labels[idx]
~~~

### Data Splitting
1. Split the data into training and testing sets using `split_data`.
2. Combined face and non-face data.
3. Re-shuffle the combined dataset
~~~ Python
def train_test_split(X, y, test_size=0.3, random_state = 42):
    # number of features
    m, n = X.shape
    # train size
    tsize = int(test_size * X.shape[0]) - 1    
    X_train, X_test, y_train, y_test = [], [], [], []
     ....
    # transform into np arrayes
    X_train, X_test, y_train, y_test = np.array(X_train), np.array(X_test), np.array(y_train), np.array(y_test)
    return X_train, X_test, y_train, y_test
~~~

   
## Usage
This project can be used to recognize faces and non-faces in images. The model is trained on a dataset of face and non-face images, and it can predict whether a new image is a face or not.

The code includes functions for loading and preprocessing the images, splitting the data into training and testing sets, applying PCA and LDA, and training and evaluating different classifiers.

## Contributing
If you want to contribute to this project, please fork the repository and make a pull request. We're always looking for new contributors!

## License
