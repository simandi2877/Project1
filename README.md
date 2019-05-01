# Assignment1B

- What are Channels and Kernels (according to EVA)?

  - Channels are similar features. Kernel is a feature extractor or filter. 
  - For example, in a musical concert has features like piano, guitar, drums, song etc. These are the features of the musical concert. Each feature is called channel.  Normally, we enjoy the concert as a whole and never break down into individual components i.e do not hear piano once and then drum and then song etc. But the whole concert is made of individual features. 
  - Kernel is a feature extractor. In the above example, if we have some instrument which filters out only piano sound out of the concert - that will be called kernel/filter/feature extractor. 

  Our eye has 3 channels - Yellow, Blue and Green. But we are able to see all the colors including Red. So, given a colored image, our eye identifies the whole image. But in this process, the 3 channels in the eye identify each color and transmits the information to cortex of brain which then make sense of the whole picture. 

  But for computers to identify an image, it requires training. The computers can be trained to identify edges -> textures -> patterns -> parts of an object -> object. For this training, kernels will be used to extract various features of the images.

  

- Why should we only (well mostly) use 3x3 Kernels?

  3x3 kernels are optimized for performance on GPUs. Even GPU vendors have added accelerated processing to their GPUs for 3x3 kernels. Following is the explanation of the optimization achieved for using 3x3.

  - Channels are similar features available in an image. Kernel is the feature extractor from the channel. If there is an image of 5x5 of lion if we are shown any "leg", we cannot be sure that this "leg" belongs to lion picture. To really match the "leg" to "lion", we should see the complete picture of lion. To see the complete picture of lion, **5x5 image has to be seen which will have 25 parameters**. So, at any cost we should information of the complete image to really detect any features in it.
  - But if we use a kernel of 3x3 on 5x5 image of lion, the output is 3x3 image which has the information of the complete 5x5 but reduced to 3x3. If one more 3x3 convolutions is done on output, we get 1x1. This 1x1 layer can see the complete image. So the receptive field of 1x1 image is the complete 5x5 image and **this layer uses only 18 parameters to look at the complete image** i.e in the first convolution of 5x5 - 9 parameters are used, and in the second convolution of 3x3 - 9 parameters are used. So, this approach **reduces the number of parameters that will be used and hence runs optimally on GPU**.
  - For example if we have to **21x21 image, then we should have 21*21 = 441 parameters** to see the complete image. But if we use **3x3 kernel with convolution operation, we have to 10 layers of convolution with 9 parameters** in the kernel. **So, the total number of parameters used is 10 layers * 9 = 90 which is much lesser than 441.**

- How many times do we need to perform 3x3 convolution operation to reach 1x1 from 199x199 (show calculations)

  - There will be 99 convolution operations on 199x199 image size to reach 1x1.
  - 197x197  | 195x195  | 193x193 | 191x191 | 189x 189 | 187x187 | 185x185 | 183x183 | 181x181 | 179x179 | 177x177 | 175x175 | 173x173 | 171x171 | 169x169 | 167x167 | 165x165 | 163x163 | 161x161 | 159x159 | 157x157 | 155x155 | 153x153 | 151x151 | 149x 149| 147x147 | 145x145 | 143x143 | 141x141 | 139x139 | 137x137 | 135x135 | 133x133 | 131x131 | 129x129| 127x127 | 125x125 | 123x123 | 121x121 | 119x119 | 117x117 | 115x115 | 113x113 | 111x111 | 109x109 | 107x107 | 105x105 | 103x103 | 101x101 | 99x99 | 97x97 | 95x95 | 93x93 | 91x91 | 89x89 | 87x87 | 85x85 | 83x83 | 81x81 | 79x79 | 77x77 | 75x75 | 73x73 | 71x71 | 69x69 | 67x67 | 65x65 | 63x63 | 61x61 | 59x59 | 57x57 | 55x55 | 53x53 | 51x51 | 49x49 | 47x47 | 45x45 | 43x43 | 41x41 | 39x39 | 37x37 | 35x35 | 33x33 | 31x31 | 29x29 | 27x27 | 25x25 | 23x23 | 21x21 | 19x19 | 17x17 | 15x15 | 13x13 | 11x11 | 9x9 | 7x7 | 5x5 | 3x3 | 1x1