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

Then I have the encoder and decoder blocks as shown below. The encoder blocks are separable convolution using batch normilization and ReLu activation. I used four encoders. The second encoder did not increase the number of filters but I did want to reduce the data information for the training so I used the same encoder parameters as encoder 1 in order to do that. 
![encoder](Screenshots/encoder.png)

The decoder concatenated the previous layer with a larger layer and then pass that concatenated data to the convolution with batch norm and ReLu activation. 
![decoder](Screenshots/decoder.png)

Finally the softmax function is called to complete the FCN using same padding.
Here I have shown the full model in the screen shot both here in coding:
![fcn_model](Screenshots/fcn_model.png)

And here I have drawn out the architecture on paper.

![Network](Screenshots/network.jpg)

#Parameters

The next work after desgining the network architecture was to determine the parameters, at first I tested several parameters schemes by only adjusting the learning rate (.01,.001, .0001), the batch size (16, 32, 20, 25) and the number of epochs (50,100,200,250). 

The learning rate would lower the score of the program if it was too low or too high. I settled on .001 as .01 was causing the network to identify nothing and .0001 was too small of a learning rate to actual create any gradients.

The batch size affected both the validation error and also if the batch size was too small, I found that I wasn't really achieving any minama's for the validation error. This greatly affected my final score.

After multiple combinations of these I was still hitting around .38 for the score (which i will explain what the score means below). I was trying to achieve .40 or higher. I was finding that if I increased the number of steps per epoch, I would reduce the validation error very quickly per epoch. This would then reduce my number of epochs needed to run the architecture and create a decent model that would recognize the target and differentiate between target and other items/people.



So I 


