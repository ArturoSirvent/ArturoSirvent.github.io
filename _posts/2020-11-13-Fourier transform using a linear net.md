---
title: "Fourier Transform performed in a Neural Network"
date: 13/11/2020
tags: [NN, fourier, deep learning,linear combination,filters]
excerpt: "How it is the Fourier transform implemented into a NN."
mathjax: "true"
---


**First we should get make the training set:**

This can be done easily performing the (discrete) fast fourier transform to a set data randomly distributed.
Realize that the discrete fourier transformation is nothing but a linear combination with a very concrete coefficients.

$$A_k =  \sum_{m=0}^{n-1} a_m \exp\left\{-2\pi i{mk \over n}\right\} \qquad k = 0,\ldots,n-1.$$

Where $$A_k$$ (vector elements in the momentum space) is made of lineary combining $$a_m$$ weighted with $$\exp\left\{-2\pi i{mk \over n}\right\}$$ , those coefficients can be obtained even before knowing the $$a_m$$ data. That means it can be seen as a vector transformation, done by a known matrix $$M$$, applied to a vector $$a$$ which finally gives the desired vector $$A$$.

$$ A = M a$$

Also we should know that a neural network with no activation function (non-linear functions) can be seen as a linear combination of the inputs.
*(Even if the NN has more than one layer, the whole proccess can be summed up to a one layer NN without activation functions.)*



That is why we use just one fully connected layer and no activation function is needed.

**The implementation is as follows:**

Remember that the fourier transform is a certain operation performed on some set of **complex** values, and gives us a complex value as well.
This complex values may be a problem for implementation on NN, but we can simply "flatten" the comple values into a 1-D array.

$$((a_1+ib_1),(a_2+ib_2),(a_3+ib_3),(a_4+ib_4),...,(a_n+ib_n)) \rightarrow (a_1,a_2,a_3,a_4,...,a_n,b_1,b_2,b_3,b_4,...,b_n)$$

```python
#variables
N=10000
input_size=96
data=[]
labels=[]
 
for i in range(N):
  data_aux=np.random.rand(input_size)+1j*np.random.rand(input_size)
  data.append(np.concatenate((data_aux.real,data_aux.imag)))
  labels_aux=np.fft.fft(data_aux)
  labels.append(np.concatenate((labels_aux.real,labels_aux.imag)))
  data.append(data_aux)
  
```

Also we need some validation data:
```python

N_val=int(N*0.2)
val_data=[]
labels_val=[]

for i in range(N_val):
  data_aux=np.random.rand(input_size)*100#+1j*np.random.rand(input_size)
  val_data.append(data_aux)
  #val_data.append(np.concatenate((data_aux.real,data_aux.imag)))
  labels_aux=np.fft.fft(data_aux)
  labels_val.append(np.append(labels_aux.real,labels_aux.imag))
 
 
```

Now we create the DataSet object we will pass in to the keras network:

```python
df=tf.data.Dataset.from_tensor_slices((data,labels))
df=df.batch(64)
df_val=tf.data.Dataset.from_tensor_slices((val_data,labels_val))
df_val=df_val.batch(64)
```

*(It is very important the batch creation, if not included it may give us error due a dimensions inconsistency, specially if the input and output shapes do no t match, it may be the case of a compresion of info or a fourier transform only for real input, but as we will se, the output stills having complex part)*

**We create the model:**

```python

model=tf.keras.Sequential([tf.keras.layers.Dense(input_size*2,use_bias=False)])
model.compile(optimizer="adam",loss="mse",metrics=["acc"])
no_performance=tf.keras.callbacks.EarlyStopping(patience=10)
epochs=100
history=model.fit(df,epochs=epochs,batch_size=32,validation_data=df_val,callbacks=[sin_mejora])
```


All this post is my own replication of the results shown in <a href="https://gist.github.com/endolith/98863221204541bf017b6cae71cb0a89">here</a> :
<script src="https://gist.github.com/endolith/98863221204541bf017b6cae71cb0a89.js"></script>
