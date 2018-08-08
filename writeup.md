# Deep Learning
## Divya Patel

In this project we train a fully conventional network to find and track ("Follow") a target. In this case, we have identified our target as a person dressed in red. The person is on a specific path and the quadcopter will patrol on its on path until the target is identified and locked in. The idenfitication of the target and the ability to follow the target is based of of the model that we capture from our network training.

Here I show the picture of when I was training the network from a far distance. You can see green quadcopter patrol points, pink target movement path and blue spawn initial paths.
![Virtual_World](ScreenShots/recording.png)

Convolution networks stack CONV (both normal and separable), POOL, and FC layers. Most convolution networks have smaller filters and deep architectures which we will be using today. I would like to try to use ResNet. I found that if I used a ResNet in the future, my error would be much smaller due to the multiplation of the derivative and the addition of that information back to it. I think there is less information lost and the network model is calculated much faster. You can see these two slides from Andrej Karpathy's lecture slides. I found his lectures extremely helpful to learn FCNs. 

![Wild_FCNS](ScreenShots/wild_fcns.png)
![Res_Net vs Conv Net](ScreenShots/res_net.png)

On to our designed network. For this, I wanted to reduce the amount of data I used so I drove a small filter with a stride of two twice in the beggining to really reduce the amount of information before deepening the network. I increased the depth of the network by double the last encoder for the 1x1 because with many more choices, i felt the network could have a better chance of identifying the target. Of course, this slowed down my calculation a bit, but with AWS I didn't have much trouble. It increased my calculation time by about one third.

###Project Code
Here the Udacity helped coding of Separable Conv Batch Norm layers are used with same padding and ReLU activation.
![Conv_Layer](ScreenShots/batchnorm.png)

For binlinear sampling, it was left as and upsampling of 2.
![Up_Sample](ScreenShots/upsample.png)

Then I have the encoder and decoder blocks as shown below. The encoder blocks are separable convolution using batch normilization and ReLu activation. I used four encoders. The second encoder did not increase the number of filters but I did want to reduce the data information for the training so I used the same encoder parameters as encoder 1 in order to do that. The decoder concatenated the previous layer with a 




