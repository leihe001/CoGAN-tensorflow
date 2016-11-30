# CoGAN-tensorflow
Implement Coupled Generative Adversarial Networks, [[NIPS 2016]](https://arxiv.org/abs/1606.07536)   
This implementation is a little bit different from the original [caffe code](https://github.com/mingyuliutw/CoGAN). Basically, I follow the model architecture design of [DCGAN](https://arxiv.org/abs/1511.06434).

## What's CoGAN?
CoGAN can learn a **joint distribution** with just samples drawn from the marginal distributions. This is achieved by enforcing a **weight-sharing constraint** that limits the network capacity and favors a joint distribution solution over a product of marginal distributions one.   
The following figure is the result showed in paper:
![](https://github.com/andrewliao11/CoGAN-tensorflow/blob/master/illustration.png?raw=true)

- Note that all the natural images here is unpaired. In a nutshell, in each training process, the input of the descriminator is not aligned.
- The experiment result of UDA problem is very impressive, which inpires me to implement this in Tensorflow.

## Requirement

- Python 2.7
- Tensorlfow

## Kick off
First you have to clone this repo:
```
$ git clone https://github.com/andrewliao11/CoGAN-tensorflow.git
```
Download the data:   
This step will automatically download the data under the current folder.
```
$ python download.py mnist
```
Preprocess(invert) the data:
```
$ python invert.py 
```
Train your CoGAN:
```
$ python main.py --is_train True
```
During the training process, you can see the average loss of the generators and the discriminators, which can hellp your debugging. After training, it will save some sample to the ```./samples/top and ./samples/bot```, respectively. 

To visualize the the whole training process, you can use Tensorboard:
```
tensorboard --logdir=logs
```
![](https://github.com/andrewliao11/CoGAN-tensorflow/blob/master/vis.png?raw=true)

## Results

- model in 9th epoch   
![](https://github.com/andrewliao11/CoGAN-tensorflow/blob/master/top_train_09_0085.png?raw=true)
![](https://github.com/andrewliao11/CoGAN-tensorflow/blob/master/bot_train_09_0085.png?raw=true)

- model in 19th epoch   
![](https://github.com/andrewliao11/CoGAN-tensorflow/blob/master/top_train_19_0025.png?raw=true)
![](https://github.com/andrewliao11/CoGAN-tensorflow/blob/master/bot_train_19_0025.png?raw=true)

We can see that without paired infomation, the network can generate two different images with the same high-level concepts.   
***Note: To avoid the fast convergence of D (discriminator) network, G (generator) network is updated twice for each D network update, which differs from original paper.***


## TODOs

- Modify the network structure to get the better results
- Try to use in different dataset

## Reference
This code is heavily built on these repo:   
- [DCGAN-tensorflow](https://github.com/carpedm20/DCGAN-tensorflow) from @carpedm20 
- [CoGAN](https://github.com/mingyuliutw/CoGAN) from @mingyuliutw
