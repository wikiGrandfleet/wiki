<!-- TITLE: Ml Matplot Lib Ex -->
<!-- SUBTITLE: A quick summary of Ml Matplot Lib Ex -->

# Header

```python

# Visualizing sample images from the dataset
## Importing the UCI ML hand-written digits dataset


```python
from sklearn.datasets import load_digits
```


```python
digits = load_digits()
```


```python
print(type(digits))
```

    <class 'sklearn.utils.Bunch'>
    


```python
print(digits)
```

    {'data': array([[  0.,   0.,   5., ...,   0.,   0.,   0.],
           [  0.,   0.,   0., ...,  10.,   0.,   0.],
           [  0.,   0.,   0., ...,  16.,   9.,   0.],
           ..., 
           [  0.,   0.,   1., ...,   6.,   0.,   0.],
           [  0.,   0.,   2., ...,  12.,   0.,   0.],
           [  0.,   0.,  10., ...,  12.,   1.,   0.]]), 'target': array([0, 1, 2, ..., 8, 9, 8]), 'target_names': array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9]), 'images': array([[[  0.,   0.,   5., ...,   1.,   0.,   0.],
            [  0.,   0.,  13., ...,  15.,   5.,   0.],
            [  0.,   3.,  15., ...,  11.,   8.,   0.],
            ..., 
            [  0.,   4.,  11., ...,  12.,   7.,   0.],
            [  0.,   2.,  14., ...,  12.,   0.,   0.],
            [  0.,   0.,   6., ...,   0.,   0.,   0.]],
    
           [[  0.,   0.,   0., ...,   5.,   0.,   0.],
            [  0.,   0.,   0., ...,   9.,   0.,   0.],
            [  0.,   0.,   3., ...,   6.,   0.,   0.],
            ..., 
            [  0.,   0.,   1., ...,   6.,   0.,   0.],
            [  0.,   0.,   1., ...,   6.,   0.,   0.],
            [  0.,   0.,   0., ...,  10.,   0.,   0.]],
    
           [[  0.,   0.,   0., ...,  12.,   0.,   0.],
            [  0.,   0.,   3., ...,  14.,   0.,   0.],
            [  0.,   0.,   8., ...,  16.,   0.,   0.],
            ..., 
            [  0.,   9.,  16., ...,   0.,   0.,   0.],
            [  0.,   3.,  13., ...,  11.,   5.,   0.],
            [  0.,   0.,   0., ...,  16.,   9.,   0.]],
    
           ..., 
           [[  0.,   0.,   1., ...,   1.,   0.,   0.],
            [  0.,   0.,  13., ...,   2.,   1.,   0.],
            [  0.,   0.,  16., ...,  16.,   5.,   0.],
            ..., 
            [  0.,   0.,  16., ...,  15.,   0.,   0.],
            [  0.,   0.,  15., ...,  16.,   0.,   0.],
            [  0.,   0.,   2., ...,   6.,   0.,   0.]],
    
           [[  0.,   0.,   2., ...,   0.,   0.,   0.],
            [  0.,   0.,  14., ...,  15.,   1.,   0.],
            [  0.,   4.,  16., ...,  16.,   7.,   0.],
            ..., 
            [  0.,   0.,   0., ...,  16.,   2.,   0.],
            [  0.,   0.,   4., ...,  16.,   2.,   0.],
            [  0.,   0.,   5., ...,  12.,   0.,   0.]],
    
           [[  0.,   0.,  10., ...,   1.,   0.,   0.],
            [  0.,   2.,  16., ...,   1.,   0.,   0.],
            [  0.,   0.,  15., ...,  15.,   0.,   0.],
            ..., 
            [  0.,   4.,  16., ...,  16.,   6.,   0.],
            [  0.,   8.,  16., ...,  16.,   8.,   0.],
            [  0.,   1.,   8., ...,  12.,   1.,   0.]]]), 'DESCR': "Optical Recognition of Handwritten Digits Data Set\n===================================================\n\nNotes\n-----\nData Set Characteristics:\n    :Number of Instances: 5620\n    :Number of Attributes: 64\n    :Attribute Information: 8x8 image of integer pixels in the range 0..16.\n    :Missing Attribute Values: None\n    :Creator: E. Alpaydin (alpaydin '@' boun.edu.tr)\n    :Date: July; 1998\n\nThis is a copy of the test set of the UCI ML hand-written digits datasets\nhttp://archive.ics.uci.edu/ml/datasets/Optical+Recognition+of+Handwritten+Digits\n\nThe data set contains images of hand-written digits: 10 classes where\neach class refers to a digit.\n\nPreprocessing programs made available by NIST were used to extract\nnormalized bitmaps of handwritten digits from a preprinted form. From a\ntotal of 43 people, 30 contributed to the training set and different 13\nto the test set. 32x32 bitmaps are divided into nonoverlapping blocks of\n4x4 and the number of on pixels are counted in each block. This generates\nan input matrix of 8x8 where each element is an integer in the range\n0..16. This reduces dimensionality and gives invariance to small\ndistortions.\n\nFor info on NIST preprocessing routines, see M. D. Garris, J. L. Blue, G.\nT. Candela, D. L. Dimmick, J. Geist, P. J. Grother, S. A. Janet, and C.\nL. Wilson, NIST Form-Based Handprint Recognition System, NISTIR 5469,\n1994.\n\nReferences\n----------\n  - C. Kaynak (1995) Methods of Combining Multiple Classifiers and Their\n    Applications to Handwritten Digit Recognition, MSc Thesis, Institute of\n    Graduate Studies in Science and Engineering, Bogazici University.\n  - E. Alpaydin, C. Kaynak (1998) Cascading Classifiers, Kybernetika.\n  - Ken Tang and Ponnuthurai N. Suganthan and Xi Yao and A. Kai Qin.\n    Linear dimensionalityreduction using relevance weighted LDA. School of\n    Electrical and Electronic Engineering Nanyang Technological University.\n    2005.\n  - Claudio Gentile. A New Approximate Maximal Margin Classification\n    Algorithm. NIPS. 2000.\n"}
    


```python
print(digits.images.shape)
```

    (1797, 8, 8)
    


```python
indices = []
for i in range(10):
    for j in digits.target:
        if i==j:
            indices.append(j)
            break
print(indices)
```

    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
    


```python
%matplotlib inline
import matplotlib.pyplot as plt
plt.scatter(list(range(200)),digits.target[:200])
plt.show()
```


![png](output_7_0.jpg)

![Output 15 0](/uploads/tutorials/output-15-0.jpg "Output 15 0")![Output 15 0](/uploads/tutorials/output-15-0.jpg "Output 15 0")

```python
import matplotlib.pyplot as plt

nrows, ncols = 2, 5
plt.figure(figsize=(6,3))

for i in range(ncols * nrows):
    ax = plt.subplot(nrows, ncols, i + 1)
    ax.imshow(digits.images[i],cmap='gray_r')
    plt.xticks([])
    plt.yticks([])
    plt.title(digits.target[i])
```


![png](/uploads/tutorials/output_8_0.jpg)


---
# Exploring the data nature by t-SNE method


```python
from sklearn.manifold import TSNE
```

---
# Creating a Convolutional Neural Network to recognize digits 


```python
import numpy as np
X = np.vstack([digits.data[digits.target==i]for i in range(10)])
y = np.hstack([digits.target[digits.target==i] for i in range(10)])
```


```python
%%timeit
#Here we run tSNE with 250 iteractions and time it
tsne_iter_250 = TSNE(init='pca',method='exact',n_components=2,n_iter=250).fit_transform(X)
```

    53.9 s ± 4.13 s per loop (mean ± std. dev. of 7 runs, 1 loop each)
    


```python
tsne_iter_250 = TSNE(init='pca',method='exact',n_components=2,n_iter=250).fit_transform(X)
```


```python
#We import the pandas and matplotlib libraries
import pandas as pd
import matplotlib
matplotlib.style.use('seaborn')
#Here we plot the tSNE results in a reduced two-dimensional space
df = pd.DataFrame(tsne_iter_250)
plt.scatter(df[0],df[1],c=y,cmap=matplotlib.cm.get_cmap('tab10'))
plt.show()
```


![png](output_15_0.jpg)



```python
#Here we run tSNE for 2000 iteractions
tsne_iter_2000 = TSNE(init='pca',method='exact',n_components=2,n_iter=2000).fit_transform(X)
#Here we plot the figure
df2 = pd.DataFrame(tsne_iter_2000)
plt.scatter(df2[0],df2[1],c=y,cmap=matplotlib.cm.get_cmap('tab10'))
plt.show()
```


![png](/uploads/tutorials/output_16_0.jpg)


---
# Creating a Convolutional Neural Network to recognize digits


```python
from sklearn.model_selection import train_test_split 
from sklearn.preprocessing import LabelBinarizer
lb = LabelBinarizer()
X = np.expand_dims(digits.images.T, axis=0).T
y = lb.fit_transform(digits.target)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=100)
```


```python
# Import sklearn models for preprocessing input data
from sklearn.model_selection import train_test_split 
from sklearn.preprocessing import LabelBinarizer

# Import the necessary Keras libraries
from keras.models import Sequential
from keras.layers import Dense, Dropout, Flatten
from keras.layers.convolutional import Convolution2D, MaxPooling2D
from keras import backend as K
from keras.callbacks import History 

# Randomize and split data into training dataset with right format to feed to Keras
lb = LabelBinarizer()
X = np.expand_dims(digits.images.T, axis=0).T
y = lb.fit_transform(digits.target)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=100)

# Start a Keras sequential model
model = Sequential()

# Set input format shape as (batch, height, width, channels)
K.set_image_data_format('channels_last') 

model.add(Convolution2D(filters=4,kernel_size=(3,3),padding='same',input_shape=(8,8,1),activation='relu'))
model.add(MaxPooling2D(pool_size=(2,2)))

# Drop out 5% of training data in each batch
model.add(Flatten())
model.add(Dropout(0.05))
model.add(Dense(10, activation= 'softmax'))

# Set variable 'history' to store callbacks to track the validation loss
history = History()

# Compile the model
model.compile(loss='categorical_crossentropy', optimizer='adam', metrics=['accuracy'])

# Fit the model and save the callbacks of validation loss and accuracy to 'history'
model.fit(X_train,y_train, epochs=100, batch_size= 128, callbacks=[history])
```

    Using TensorFlow backend.
    

    Epoch 1/100
    1437/1437 [==============================] - 0s - loss: 8.1692 - acc: 0.0682     
    Epoch 2/100
    1437/1437 [==============================] - 0s - loss: 6.1486 - acc: 0.0891     
    Epoch 3/100
    1437/1437 [==============================] - 0s - loss: 4.9665 - acc: 0.0953     
    Epoch 4/100
    1437/1437 [==============================] - 0s - loss: 4.3481 - acc: 0.1113     
    Epoch 5/100
    1437/1437 [==============================] - 0s - loss: 3.6783 - acc: 0.1580     
    Epoch 6/100
    1437/1437 [==============================] - 0s - loss: 3.1635 - acc: 0.2164     
    Epoch 7/100
    1437/1437 [==============================] - 0s - loss: 2.7373 - acc: 0.2568     
    Epoch 8/100
    1437/1437 [==============================] - 0s - loss: 2.4488 - acc: 0.3173     
    Epoch 9/100
    1437/1437 [==============================] - 0s - loss: 2.2028 - acc: 0.3633     
    Epoch 10/100
    1437/1437 [==============================] - 0s - loss: 1.8948 - acc: 0.4196     
    Epoch 11/100
    1437/1437 [==============================] - 0s - loss: 1.6945 - acc: 0.4739     
    Epoch 12/100
    1437/1437 [==============================] - 0s - loss: 1.5266 - acc: 0.4969     
    Epoch 13/100
    1437/1437 [==============================] - 0s - loss: 1.3605 - acc: 0.5602     
    Epoch 14/100
    1437/1437 [==============================] - 0s - loss: 1.2421 - acc: 0.6103     
    Epoch 15/100
    1437/1437 [==============================] - 0s - loss: 1.1508 - acc: 0.6395     
    Epoch 16/100
    1437/1437 [==============================] - 0s - loss: 1.0630 - acc: 0.6451     
    Epoch 17/100
    1437/1437 [==============================] - 0s - loss: 0.9845 - acc: 0.6646     
    Epoch 18/100
    1437/1437 [==============================] - 0s - loss: 0.9346 - acc: 0.7001     
    Epoch 19/100
    1437/1437 [==============================] - 0s - loss: 0.8719 - acc: 0.7112     
    Epoch 20/100
    1437/1437 [==============================] - 0s - loss: 0.8102 - acc: 0.7258     
    Epoch 21/100
    1437/1437 [==============================] - 0s - loss: 0.7771 - acc: 0.7411     
    Epoch 22/100
    1437/1437 [==============================] - 0s - loss: 0.7472 - acc: 0.7446     
    Epoch 23/100
    1437/1437 [==============================] - 0s - loss: 0.6992 - acc: 0.7662     
    Epoch 24/100
    1437/1437 [==============================] - 0s - loss: 0.6888 - acc: 0.7655     
    Epoch 25/100
    1437/1437 [==============================] - 0s - loss: 0.6513 - acc: 0.7912     
    Epoch 26/100
    1437/1437 [==============================] - 0s - loss: 0.6306 - acc: 0.7829     
    Epoch 27/100
    1437/1437 [==============================] - 0s - loss: 0.5693 - acc: 0.8177     
    Epoch 28/100
    1437/1437 [==============================] - 0s - loss: 0.5322 - acc: 0.8170     
    Epoch 29/100
    1437/1437 [==============================] - 0s - loss: 0.5639 - acc: 0.8058     
    Epoch 30/100
    1437/1437 [==============================] - 0s - loss: 0.5697 - acc: 0.8191     
    Epoch 31/100
    1437/1437 [==============================] - 0s - loss: 0.5057 - acc: 0.8274     
    Epoch 32/100
    1437/1437 [==============================] - 0s - loss: 0.4682 - acc: 0.8372     
    Epoch 33/100
    1437/1437 [==============================] - 0s - loss: 0.4394 - acc: 0.8455     
    Epoch 34/100
    1437/1437 [==============================] - 0s - loss: 0.4450 - acc: 0.8553     
    Epoch 35/100
    1437/1437 [==============================] - 0s - loss: 0.4404 - acc: 0.8580     
    Epoch 36/100
    1437/1437 [==============================] - 0s - loss: 0.4405 - acc: 0.8448     
    Epoch 37/100
    1437/1437 [==============================] - 0s - loss: 0.4057 - acc: 0.8643     
    Epoch 38/100
    1437/1437 [==============================] - 0s - loss: 0.4228 - acc: 0.8559     
    Epoch 39/100
    1437/1437 [==============================] - 0s - loss: 0.4119 - acc: 0.8587     
    Epoch 40/100
    1437/1437 [==============================] - 0s - loss: 0.3782 - acc: 0.8664     
    Epoch 41/100
    1437/1437 [==============================] - 0s - loss: 0.3687 - acc: 0.8775     
    Epoch 42/100
    1437/1437 [==============================] - 0s - loss: 0.3877 - acc: 0.8664     
    Epoch 43/100
    1437/1437 [==============================] - 0s - loss: 0.3585 - acc: 0.8789     
    Epoch 44/100
    1437/1437 [==============================] - 0s - loss: 0.3610 - acc: 0.8761     
    Epoch 45/100
    1437/1437 [==============================] - 0s - loss: 0.3506 - acc: 0.8824     
    Epoch 46/100
    1437/1437 [==============================] - 0s - loss: 0.3342 - acc: 0.8887     
    Epoch 47/100
    1437/1437 [==============================] - 0s - loss: 0.3104 - acc: 0.8873     
    Epoch 48/100
    1437/1437 [==============================] - 0s - loss: 0.3141 - acc: 0.8977     
    Epoch 49/100
    1437/1437 [==============================] - 0s - loss: 0.3227 - acc: 0.8928     
    Epoch 50/100
    1437/1437 [==============================] - 0s - loss: 0.3152 - acc: 0.8907     
    Epoch 51/100
    1437/1437 [==============================] - 0s - loss: 0.3211 - acc: 0.8907     
    Epoch 52/100
    1437/1437 [==============================] - 0s - loss: 0.3015 - acc: 0.8991     
    Epoch 53/100
    1437/1437 [==============================] - 0s - loss: 0.3039 - acc: 0.9047     
    Epoch 54/100
    1437/1437 [==============================] - 0s - loss: 0.3027 - acc: 0.8991     
    Epoch 55/100
    1437/1437 [==============================] - 0s - loss: 0.3003 - acc: 0.8984     
    Epoch 56/100
    1437/1437 [==============================] - 0s - loss: 0.2743 - acc: 0.9102     
    Epoch 57/100
    1437/1437 [==============================] - 0s - loss: 0.2943 - acc: 0.9068     
    Epoch 58/100
    1437/1437 [==============================] - 0s - loss: 0.2549 - acc: 0.9165     
    Epoch 59/100
    1437/1437 [==============================] - 0s - loss: 0.2763 - acc: 0.9068     
    Epoch 60/100
    1437/1437 [==============================] - 0s - loss: 0.2691 - acc: 0.9054     
    Epoch 61/100
    1437/1437 [==============================] - 0s - loss: 0.2656 - acc: 0.9109     
    Epoch 62/100
    1437/1437 [==============================] - 0s - loss: 0.2628 - acc: 0.9172     
    Epoch 63/100
    1437/1437 [==============================] - 0s - loss: 0.2658 - acc: 0.9012     
    Epoch 64/100
    1437/1437 [==============================] - 0s - loss: 0.2972 - acc: 0.8963     
    Epoch 65/100
    1437/1437 [==============================] - 0s - loss: 0.2474 - acc: 0.9255     
    Epoch 66/100
    1437/1437 [==============================] - 0s - loss: 0.2530 - acc: 0.9207     
    Epoch 67/100
    1437/1437 [==============================] - 0s - loss: 0.2718 - acc: 0.9081     
    Epoch 68/100
    1437/1437 [==============================] - 0s - loss: 0.2345 - acc: 0.9276     
    Epoch 69/100
    1437/1437 [==============================] - 0s - loss: 0.2356 - acc: 0.9241     
    Epoch 70/100
    1437/1437 [==============================] - 0s - loss: 0.2325 - acc: 0.9193     
    Epoch 71/100
    1437/1437 [==============================] - 0s - loss: 0.2383 - acc: 0.9248     
    Epoch 72/100
    1437/1437 [==============================] - 0s - loss: 0.2162 - acc: 0.9214     
    Epoch 73/100
    1437/1437 [==============================] - 0s - loss: 0.2195 - acc: 0.9311     
    Epoch 74/100
    1437/1437 [==============================] - 0s - loss: 0.2170 - acc: 0.9325     
    Epoch 75/100
    1437/1437 [==============================] - 0s - loss: 0.2335 - acc: 0.9200     
    Epoch 76/100
    1437/1437 [==============================] - 0s - loss: 0.2138 - acc: 0.9339     
    Epoch 77/100
    1437/1437 [==============================] - 0s - loss: 0.2173 - acc: 0.9228     
    Epoch 78/100
    1437/1437 [==============================] - 0s - loss: 0.2003 - acc: 0.9304     
    Epoch 79/100
    1437/1437 [==============================] - 0s - loss: 0.2071 - acc: 0.9290     
    Epoch 80/100
    1437/1437 [==============================] - 0s - loss: 0.1944 - acc: 0.9402     
    Epoch 81/100
    1437/1437 [==============================] - 0s - loss: 0.2126 - acc: 0.9255     
    Epoch 82/100
    1437/1437 [==============================] - 0s - loss: 0.1863 - acc: 0.9457     
    Epoch 83/100
    1437/1437 [==============================] - 0s - loss: 0.1908 - acc: 0.9408     
    Epoch 84/100
    1437/1437 [==============================] - 0s - loss: 0.2044 - acc: 0.9360     
    Epoch 85/100
    1437/1437 [==============================] - 0s - loss: 0.2146 - acc: 0.9248     
    Epoch 86/100
    1437/1437 [==============================] - 0s - loss: 0.2030 - acc: 0.9332     
    Epoch 87/100
    1437/1437 [==============================] - 0s - loss: 0.1942 - acc: 0.9346     
    Epoch 88/100
    1437/1437 [==============================] - 0s - loss: 0.1982 - acc: 0.9318     
    Epoch 89/100
    1437/1437 [==============================] - 0s - loss: 0.1878 - acc: 0.9422     
    Epoch 90/100
    1437/1437 [==============================] - 0s - loss: 0.1916 - acc: 0.9290     
    Epoch 91/100
    1437/1437 [==============================] - 0s - loss: 0.2054 - acc: 0.9325     
    Epoch 92/100
    1437/1437 [==============================] - 0s - loss: 0.1831 - acc: 0.9408     
    Epoch 93/100
    1437/1437 [==============================] - 0s - loss: 0.1776 - acc: 0.9457     
    Epoch 94/100
    1437/1437 [==============================] - 0s - loss: 0.1832 - acc: 0.9346     
    Epoch 95/100
    1437/1437 [==============================] - 0s - loss: 0.1727 - acc: 0.9402     
    Epoch 96/100
    1437/1437 [==============================] - 0s - loss: 0.1785 - acc: 0.9478     
    Epoch 97/100
    1437/1437 [==============================] - 0s - loss: 0.1624 - acc: 0.9471     
    Epoch 98/100
    1437/1437 [==============================] - 0s - loss: 0.1664 - acc: 0.9450     
    Epoch 99/100
    1437/1437 [==============================] - 0s - loss: 0.1863 - acc: 0.9381     
    Epoch 100/100
    1437/1437 [==============================] - 0s - loss: 0.1679 - acc: 0.9415     
    




    <keras.callbacks.History at 0x142434a8>



# Evaluating prediction results with visualizations


```python
print(history.history.keys())
```

    dict_keys(['loss', 'acc'])
    


```python
import pandas as pd
import matplotlib
matplotlib.style.use('seaborn')

# Here plots the loss function graph along Epochs
pd.DataFrame(history.history['loss']).plot()
plt.legend([])
plt.xlabel('Epoch')
plt.ylabel('Loss')
plt.title('Validation loss across 100 epochs',fontsize=20,fontweight='bold')
plt.show()

# Here plots the percentage of accuracy along Epochs
pd.DataFrame(history.history['acc']).plot()
plt.legend([])
plt.xlabel('Epoch')
plt.ylabel('Accuracy')
plt.title('Accuracy loss across 100 epochs',fontsize=20,fontweight='bold')
plt.show()
```


![png](/uploads/tutorials/output_22_0.jpg)



![png](/uploads/tutorials/output_22_1.jpg)


---
## Examining the prediction performance for each digit 


```python
y_test1 = model.predict(X_test)
y_test1 = lb.fit_transform(np.round(y_test1))
y_test1 = np.argmax(y_test1, axis=1)
y_test = np.argmax(y_test, axis=1)
```


```python
import numpy as np
mislabeled_indices = np.arange(len(y_test))[y_test!=y_test1]
true_labels = np.asarray([y_test[i] for i in mislabeled_indices])
predicted_labels = np.asarray([y_test1[i] for i in mislabeled_indices])
print(mislabeled_indices)
print(true_labels)
print(predicted_labels)
```

    [  0  56  80 117 134 135 146 189 192 198 202 237 291 294 323 335]
    [9 8 1 4 8 2 8 8 4 8 9 3 7 6 8 8]
    [8 5 0 9 0 0 0 0 9 1 0 7 9 8 9 3]
    


```python
mislabeled_digit_counts = [len(true_labels[true_labels==i]) for i in range(10)]
mislabeled_digit_counts 
```




    [0, 1, 1, 1, 2, 0, 1, 1, 7, 2]




```python
total_digit_counts = [len(y_test[y_test==i]) for i in range(10)]
total_digit_counts
```




    [42, 32, 41, 32, 36, 35, 40, 39, 27, 36]




```python
mislabeled_ratio = [mislabeled_digit_counts[i]/total_digit_counts[i] for i in range(10)]
mislabeled_ratio
```




    [0.0,
     0.03125,
     0.024390243902439025,
     0.03125,
     0.05555555555555555,
     0.0,
     0.025,
     0.02564102564102564,
     0.25925925925925924,
     0.05555555555555555]




```python
pd.DataFrame(mislabeled_ratio).plot(kind='bar')
plt.xticks(rotation=0)
plt.xlabel('Digit')
plt.ylabel('Mislabeled ratio')
plt.legend([])
plt.show()
```


![png/uploads/tutorials/output_29_0.jpg)


---
## Extracting the falsely predicted images


```python
import matplotlib.pyplot as plt
nrows, ncols = 2, 5
plt.figure(figsize=(6,3))
for i in range(ncols * nrows):
    j = mislabeled_indices[i]
    ax = plt.subplot(nrows, ncols, i + 1)
    ax.imshow(X_test[j].reshape(8,8),cmap='gray_r')
    plt.xticks([])
    plt.yticks([])
    plt.title(y_test1[j],color='red')
    plt.xlabel(y_test[j],color='green')
plt.show()
```


![png](/uploads/tutorials/output_31_0.jpg)



```python

```
