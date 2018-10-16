---
title: 2018-10-17手把手教你用keras--CNN网络识别cifar10 
tags: 
grammar_cjkRuby: true
---
[toc!?]
## 手把手教你用keras--CNN网络识别cifar10

原创： DoubleV0203 [机器学习算法工程师](javascript:void(0);) 

   作者： 陈    扬         

编辑：黄俊嘉          

**前  言**

嗨咯，大家好，我是来自中国海洋大学的海盗船长。今天我来开系列新坑了，这段时间一直在帮璇姐跑实验代码，做了蛮多的对比实验，其中我就发现了，keras的代码实现和可阅读性很好，搭神经网络就好像搭乐高积木一样有趣哦😯。不只是demo哦，我还会在接下来的一系列keras教程中教你搭建Alexnet，Vggnet，Resnet等等实际的模型并且教你如何在GPU服务器上运行。

**01**

# **keras介绍**

Keras 是一个用 Python 编写的高级神经网络 API，它能够以 TensorFlow, CNTK, 或者 Theano 作为后端运行。Keras 的开发重点是支持快速的实验。能够以最小的时延把你的想法转换为实验结果，是做好研究的关键。

如果你在以下情况下需要深度学习库，请使用 Keras：

允许简单而快速的原型设计（由于用户友好，高度模块化，可扩展性）。

同时支持卷积神经网络和循环神经网络，以及两者的组合。

在 CPU 和 GPU 上无缝运行。

**02**

# **安装**

<pre>pip install TensorFlow 
pip install keras</pre>

**03**

# **数据集**

这一次，我们介绍的是实验室最常见的数据集，CIFAR-10，这个数据集的计算量大概是MNIST的10倍左右，用普通PC勉强也能跑，一般我们用到这个数据集了就还是会在实验室的服务器上面用GPU加速。

下载：https://www.cs.toronto.edu/~kriz/cifar.html

CIFAR-10数据集由10个类中的60000个32x32彩色图像组成，每个类有6000个图像。有50000个训练图像和10000个测试图像。 

数据集分为五个训练批次和一个测试批次，每个批次有10000个图像。测试批次包含来自每个类别的1000个随机选择的图像。训练批次以随机顺序包含剩余图像，但是一些训练批次可能包含来自一个类别的更多图像而不是另一个类别。在它们之间，训练批次包含来自每个类别的5000个图像。

在这里，我们可以发挥keras的天生优势，简易的加载数据集  

<pre>import keras
form keras.datasets import cifar10</pre>

(ps,这里我们有一调命令要在终端  

<pre>sudo apt-get install graphviz
pip install pydot</pre>

**04**

**CNN网络结构模型**

emmmm，网络结构比较深

**05**

**头文件**

<pre>#coding=utf-8
import keras
from keras.datasets import cifar10
from keras.preprocessing.image import ImageDataGenerator
from keras.models import Sequential
from keras.layers import Dense, Dropout, Flatten
from keras.layers import Conv2D, MaxPooling2D, ZeroPadding2D, GlobalMaxPooling2D</pre>

Sequential:顺序模型

Dense：全连接，简称FC

Flatten：上图中s4到c5的过程，相当于把16*5*5的feature map展开成400的特征向量，在通过全连接压成120维的特征向量

Conv2D：2d卷积

ImageDataGenerator：图片增强，keras自带的数据增强函数，可以让我们的数据集更大，训练出来的网络泛化能力更好

Dropout:drouput层，基于一定概率的神经元不激活，可以防止过拟合

Activation：激活层，通过激活函数对张量进行激活

MaxPooling2D：2d下采样，文章中的subsampling

to_categorical：把一维的向量转换为num_class维的One-hot编码

from keras.datasets import cifar10：keras自带了CIFAR-10数据集

plot_model：打印我们等下建好的模型，相当于可视化模型

**06**

**加载数据集**

<pre>batch_size = 32 
num_classes = 10
epochs = 1600
data_augmentation = True

# The data, shuffled and split between train and test sets:
(x_train, y_train), (x_test, y_test) = cifar10.load_data()
print('x_train shape:', x_train.shape)
print(x_train.shape[0], 'train samples')
print(x_test.shape[0], 'test samples')
x_train = x_train.astype('float32')
x_test = x_test.astype('float32')
x_train /= 255
x_test /= 255

# Convert class vectors to binary class matrices.
y_train = keras.utils.to_categorical(y_train, num_classes)
y_test = keras.utils.to_categorical(y_test, num_classes)</pre>

X_train,y_train：训练的样本的数据和labels

X_test,y_test： 测试的样本的数据和labels

50000 train samples

10000 test samples

x_train's shape=

(50000,32,32,3),dtype=int,0~255

y_train's shape= (50000, 10)

**07**

**搭建网络**

<pre>model = Sequential()

model.add(Conv2D(32, (3, 3), padding='same',
                input_shape=x_train.shape[1:]))
model.add(Activation('relu'))
model.add(Conv2D(32, (3, 3), padding='same',
                input_shape=x_train.shape[1:]))
model.add(Activation('relu'))
model.add(Conv2D(32, (3, 3), padding='same',
                input_shape=x_train.shape[1:]))
model.add(Activation('relu'))
model.add(Conv2D(48, (3, 3), padding='same',
                input_shape=x_train.shape[1:]))
model.add(Activation('relu'))
model.add(Conv2D(48, (3, 3), padding='same',
                input_shape=x_train.shape[1:]))
model.add(Activation('relu'))
model.add(MaxPooling2D(pool_size=(2, 2)))
model.add(Dropout(0.25))

model.add(Conv2D(80, (3, 3), padding='same',
                input_shape=x_train.shape[1:]))
model.add(Activation('relu'))
model.add(Conv2D(80, (3, 3), padding='same',
                input_shape=x_train.shape[1:]))
model.add(Activation('relu'))
model.add(Conv2D(80, (3, 3), padding='same',
                input_shape=x_train.shape[1:]))
model.add(Activation('relu'))
model.add(Conv2D(80, (3, 3), padding='same',
                input_shape=x_train.shape[1:]))
model.add(Activation('relu'))
model.add(Conv2D(80, (3, 3), padding='same',
                input_shape=x_train.shape[1:]))
model.add(Activation('relu'))
model.add(MaxPooling2D(pool_size=(2, 2)))
model.add(Dropout(0.25))

model.add(Conv2D(128, (3, 3), padding='same',
                input_shape=x_train.shape[1:]))
model.add(Activation('relu'))
model.add(Conv2D(128, (3, 3), padding='same',
                input_shape=x_train.shape[1:]))
model.add(Activation('relu'))
model.add(Conv2D(128, (3, 3), padding='same',
                input_shape=x_train.shape[1:]))
model.add(Activation('relu'))
model.add(Conv2D(128, (3, 3), padding='same',
                input_shape=x_train.shape[1:]))
model.add(Activation('relu'))
model.add(Conv2D(128, (3, 3), padding='same',
                input_shape=x_train.shape[1:]))
model.add(Activation('relu'))
model.add(GlobalMaxPooling2D())
model.add(Dropout(0.25))

model.add(Dense(500))
model.add(Activation('relu'))
model.add(Dropout(0.25))
model.add(Dense(num_classes))
model.add(Activation('softmax'))
model.summary ()</pre>

第一,二层：32个（3*3）的卷积核，步长为1（默认也是1），

第一个网络层要有input_shape参数，告诉神经网络你的输入的张量的大小是多少，我推荐的写法是X_train.shape[1:]，这样的话我换数据集就不用去换参数，网络会自适应。

data_format='channels_last'的意思是告诉keras你的channel是在前面还是后面，tensorflow后台默认是last，theano后台默认是first，我们这里是默认值（不用轻易改变，对训练时间有很大影响，要尽量符合后端的顺序，比如tensorflow后台就不用输入channels_first,如果是这样的话，实际训练还是会转成last，极大的降低速度）。

padding='same'(默认valid），表示特征图的大小是不会改变的，‘same’是周边补充空白表示特征图大小不变。

activation='relu'表示激活函数是relu，在卷积完之后运行激活函数，默认是没有。

kernel_initializer='uniform'表示卷积核为默认类型

第三层：Maxpooling，参数比较少，就一个池化核的大小，2*2，步长strides默认和池化大小一致。

第12层Dropout

keras.layers.Dropout(rate, noise_shape=None, seed=None)

将 Dropout 应用于输入。

Dropout 包括在训练中每次更新时， 将输入单元的按比率随机设置为 0， 这有助于防止过拟合。

第16层：GlobalMaxPooling2D

keras.layers.GlobalMaxPooling2D(data_format=None)

对于空域数据的全局最大池化。

输出尺寸是 (batch_size, channels) 的 2D 张量 

最后一层：Dense（10）表示把他压成和我们labels一样的维度10，通过softmax进行激活（多分类用softmax）

model.summary():打印网络结构及其内部参数

**08**

**网络结构参数**

<pre>_________________________________________________________________
Layer (type)                 Output Shape              Param #   
=================================================================
conv2d_1 (Conv2D)            (None, 32, 32, 32)        896       
_________________________________________________________________
activation_1 (Activation)    (None, 32, 32, 32)        0         
_________________________________________________________________
conv2d_2 (Conv2D)            (None, 32, 32, 32)        9248      
_________________________________________________________________
activation_2 (Activation)    (None, 32, 32, 32)        0         
_________________________________________________________________
conv2d_3 (Conv2D)            (None, 32, 32, 32)        9248      
_________________________________________________________________
activation_3 (Activation)    (None, 32, 32, 32)        0         
_________________________________________________________________
conv2d_4 (Conv2D)            (None, 32, 32, 48)        13872     
_________________________________________________________________
activation_4 (Activation)    (None, 32, 32, 48)        0         
_________________________________________________________________
conv2d_5 (Conv2D)            (None, 32, 32, 48)        20784     
_________________________________________________________________
activation_5 (Activation)    (None, 32, 32, 48)        0         
_________________________________________________________________
max_pooling2d_1 (MaxPooling2 (None, 16, 16, 48)        0         
_________________________________________________________________
dropout_1 (Dropout)          (None, 16, 16, 48)        0         
_________________________________________________________________
conv2d_6 (Conv2D)            (None, 16, 16, 80)        34640     
_________________________________________________________________
activation_6 (Activation)    (None, 16, 16, 80)        0         
_________________________________________________________________
conv2d_7 (Conv2D)            (None, 16, 16, 80)        57680     
_________________________________________________________________
activation_7 (Activation)    (None, 16, 16, 80)        0         
_________________________________________________________________
conv2d_8 (Conv2D)            (None, 16, 16, 80)        57680     
_________________________________________________________________
activation_8 (Activation)    (None, 16, 16, 80)        0         
_________________________________________________________________
conv2d_9 (Conv2D)            (None, 16, 16, 80)        57680     
_________________________________________________________________
activation_9 (Activation)    (None, 16, 16, 80)        0         
_________________________________________________________________
conv2d_10 (Conv2D)           (None, 16, 16, 80)        57680     
_________________________________________________________________
activation_10 (Activation)   (None, 16, 16, 80)        0         
_________________________________________________________________
max_pooling2d_2 (MaxPooling2 (None, 8, 8, 80)          0         
_________________________________________________________________
dropout_2 (Dropout)          (None, 8, 8, 80)          0         
_________________________________________________________________
conv2d_11 (Conv2D)           (None, 8, 8, 128)         92288     
_________________________________________________________________
activation_11 (Activation)   (None, 8, 8, 128)         0         
_________________________________________________________________
conv2d_12 (Conv2D)           (None, 8, 8, 128)         147584    
_________________________________________________________________
activation_12 (Activation)   (None, 8, 8, 128)         0         
_________________________________________________________________
conv2d_13 (Conv2D)           (None, 8, 8, 128)         147584    
_________________________________________________________________
activation_13 (Activation)   (None, 8, 8, 128)         0         
_________________________________________________________________
conv2d_14 (Conv2D)           (None, 8, 8, 128)         147584    
_________________________________________________________________
activation_14 (Activation)   (None, 8, 8, 128)         0         
_________________________________________________________________
conv2d_15 (Conv2D)           (None, 8, 8, 128)         147584    
_________________________________________________________________
activation_15 (Activation)   (None, 8, 8, 128)         0         
_________________________________________________________________
global_max_pooling2d_1 (Glob (None, 128)               0         
_________________________________________________________________
dropout_3 (Dropout)          (None, 128)               0         
_________________________________________________________________
dense_1 (Dense)              (None, 500)               64500     
_________________________________________________________________
activation_16 (Activation)   (None, 500)               0         
_________________________________________________________________
dropout_4 (Dropout)          (None, 500)               0         
_________________________________________________________________
dense_2 (Dense)              (None, 10)                5010      
_________________________________________________________________
activation_17 (Activation)   (None, 10)                0         
=================================================================
Total params: 1,071,542
Trainable params: 1,071,542
Non-trainable params: 0
_________________________________________________________________</pre>

预计使用的显存大小和计算资源

大概是10g的显存，GTX1080TI

**09**

**编译及训练**

<pre># initiate RMSprop optimizer
opt = keras.optimizers.Adam(lr=0.0001)

# Let's train the model using RMSprop
model.compile(loss='categorical_crossentropy',
             optimizer=opt,
             metrics=['accuracy'])

print("train____________")
model.fit(X_train,y_train,epochs=600,batch_size=128,)
print("test_____________")
loss,acc=model.evaluate(X_test,y_test)
print("loss=",loss)
print("accuracy=",acc)</pre>

model.compile:对模型进行编译，

optimizer是优化器，我这里选的是随机梯度下降，具体还要许多优化器，你可以上官网[查看][4]，这里使用的是Adam，学习率是0，0001，动量衰减为0

loss='categorical_crossentropy'：多分类用的one-hot交叉熵

metrics=['accuracy']：表示我们要优化的是正确率

model.fit(X_train,y_train,epochs=600,batch_size=128,)：进行600轮，批次为128的训练，默认训练过程中是会加入正则化防止过拟合。

loss,acc=model.evaluate(X_test,y_test)：对样本进行测试，默认不使用正则化，返回损失值和正确率。

**10**

**基于数据增强的训练方法**

<pre>if not data_augmentation:
   print('Not using data augmentation.')
   model.fit(x_train, y_train,
             batch_size=batch_size,
             epochs=epochs,
             validation_data=(x_test, y_test),
             shuffle=True, callbacks=[tbCallBack])
else:
   print('Using real-time data augmentation.')
   # This will do preprocessing and realtime data augmentation:
   '''
   datagen = ImageDataGenerator(
       featurewise_center=False,  # set input mean to 0 over the dataset
       samplewise_center=False,  # set each sample mean to 0
       featurewise_std_normalization=False,  # divide inputs by std of the dataset
       samplewise_std_normalization=False,  # divide each input by its std
       zca_whitening=False,  # apply ZCA whitening
       rotation_range=0,  # randomly rotate images in the range (degrees, 0 to 180)
       width_shift_range=0.1,  # randomly shift images horizontally (fraction of total width)
       height_shift_range=0.1,  # randomly shift images vertically (fraction of total height)
       horizontal_flip=True,  # randomly flip images
       vertical_flip=False)  # randomly flip images
   '''
   datagen = ImageDataGenerator(
       featurewise_center=False,  # set input mean to 0 over the dataset
       samplewise_center=False,  # set each sample mean to 0
       featurewise_std_normalization=False,  # divide inputs by std of the dataset
       samplewise_std_normalization=False,  # divide each input by its std
       zca_whitening=False,  # apply ZCA whitening
       rotation_range=10,  # randomly rotate images in the range (degrees, 0 to 180)
       width_shift_range=0.2,  # randomly shift images horizontally (fraction of total width)
       height_shift_range=0.2,  # randomly shift images vertically (fraction of total height)
       horizontal_flip=True,  # randomly flip images
       vertical_flip=False)  # randomly flip images

   # Compute quantities required for feature-wise normalization
   # (std, mean, and principal components if ZCA whitening is applied).
   datagen.fit(x_train)

   # Fit the model on the batches generated by datagen.flow().
   model.fit_generator(datagen.flow(x_train, y_train,
                                    batch_size=batch_size),
                       steps_per_epoch=x_train.shape[0] // batch_size,
                       epochs=epochs,
                       validation_data=(x_test, y_test), callbacks=[tbCallBack])</pre>

当我在我的6核心12线程酷睿i7版macbookpro15运行一个epoch时要的时间

!

对……你没看错超频543%了还有20min一个epoch，是不是感觉500个跑完就天荒地老了。

**11**

**在gpu服务器上运行**

你没看错，这就是GTX1080ti核弹的力量，在很久很久以后。

**12**

**模型的画图和图片保存**

<pre>import matplotlib.pyplot as plt
import matplotlib.image as mpimg 
from keras.utils import plot_model
plot_model(model,to_file='example.png',show_shapes=True)
lena = mpimg.imread('example.png') # 读取和代码处于同一目录下的 lena.png
#此时 lena 就已经是一个 np.array 了，可以对它进行任意处理
lena.shape #(512, 512, 3)
plt.imshow(lena) # 显示图片
plt.axis('off') # 不显示坐标轴
plt.show()</pre>

祖传模型打印代码，我觉得注释已经足够详细了

**13**

**模型的保存**

<pre>config = model.get_config()
model = model.from_config(config)</pre>

**END**

往期回顾之作者陈扬

【1】[手把手教你用keras--像搭乐高积木一样搭建神经网络（lenet）](http://mp.weixin.qq.com/s?__biz=MzUyMjE2MTE0Mw==&mid=2247487028&idx=1&sn=b90c9aa35e838d7436cf4baf1bfd1a5e&chksm=f9d150accea6d9ba29aff83c1e333429a5b1c81aaada2f92d4e5f8c2aa0fdcbb6cfdf22dc50e&scene=21#wechat_redirect)

【2】[机器学习论文笔记（七）：一种简单有效的网络结构搜索](http://mp.weixin.qq.com/s?__biz=MzUyMjE2MTE0Mw==&mid=2247487020&idx=1&sn=65548e27f9e12744174726211c3d2e25&chksm=f9d150b4cea6d9a25626c664ca8ff045aaf0c5da9e82e5aa14c5fc3cd333fdabf132b8531061&scene=21#wechat_redirect)

【3】[机器学习论文笔记-如何利用高效搜索算法来搜索网络的拓扑结构](http://mp.weixin.qq.com/s?__biz=MzUyMjE2MTE0Mw==&mid=2247486970&idx=2&sn=6878205053d13467f66055a3314eeba1&chksm=f9d15362cea6da742d2d189b6b60200138a52837c09111963922478ea954a1169aaa6774b7d4&scene=21#wechat_redirect)

【4】[近期火爆的MEta Learning，遗传算法与深度学习的火花](http://mp.weixin.qq.com/s?__biz=MzUyMjE2MTE0Mw==&mid=2247486422&idx=1&sn=cc791b957e625bb96efd38ac6c72eba0&chksm=f9d1554ecea6dc587aea5c0b6b50049b5bd6b2b6223d8dff99125f89e529f4a551c40f71da2c&scene=21#wechat_redirect)

