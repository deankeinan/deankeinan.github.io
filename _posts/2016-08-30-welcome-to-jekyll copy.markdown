---
layout: post
title:  "Feeding a neural network 19 seasons of South Park"
date:   2016-08-28 15:57:59 -0400
categories: data, machinelearning
---
# SouthPark-rnn

###Acknowledgments
This was my first time experimenting with anything machine learning and couldn't have been done without [torch-rnn](https://github.com/jcjohnson/torch-rnn), the help of this guide [here](http://www.jeffreythompson.org/blog/2016/03/25/torch-rnn-mac-install/) by Jeffrey Thompson, and of course the massive collection of data cleaned and compiled by Bob Adams [here](https://github.com/BobAdamsEE/SouthParkData). Going forward, I hope to revisit this when I've got a deeper insight into working with data.

### Training a model on 19 seasons
After a series of hiccups setting up torch-rnn on my macbook, I decided to put it to the test and trained it on a single season of South Park at first. The results were hardly coherent with the occasional whole word or phrase shining through. I don't think I got a screen grab of that but it was basically trash. 

So, I cleaned up the Bob Adams .csv (linked above) into a fat plaintext file you can find in the repository under `/data/sp-big.txt` and preprocessed it.

![alt text](https://github.com/deankeinan/SouthPark-rnn/blob/master/images/preprocessed.png "Even for 19 seasons that's a lot of Token's.")

Training the model took roughly 7 hours without enabling GPU acceleration. Thankfully it didn't melt my laptop, and I think I could have been multitasking during the process. 

## Results

*Note: 10 samples at different temperatures can be found [in the repository](https://github.com/deankeinan/SouthPark-rnn/tree/master/Samples).*

Sampling the text produced some interesting results, especially while varying the 	
`-temperature` flag (which varies the level of noise in the sample generation). 

At lower temperatures we see little to no spelling errors but highly repetitive phrasing, as you can see here:

![alt text](https://github.com/deankeinan/SouthPark-rnn/blob/master/images/temp01.png "What the hell are you doing?!")

Common words/phrases at this level: `"What the hell are you doing?", "Country", "Balls"`

Steadily increasing the temperature, we get more variance in phrasing but more spelling errors. I found at `temperature -0.7` the balance felt just right. 

![alt text](https://github.com/deankeinan/SouthPark-rnn/blob/master/images/temp07.png "Some sampled text at Temperature 0.7")

Definitely fun to read through the nonsense samples here, and maybe I could find a silly use for them. Being a fan of the show it's fun subvocalizing the nonsense in the voices of the characters. In the repository I've included a 60,000 length sample at this temperature in case anyone is looking for inspiration.

###Final Thoughts
After 19 seasons of text (roughly 5.1MB) the nonsense is of a very high degree even at lower temperatures. I mostly attribute this to the fact that I fed the entire bulk text into torch-rnn without prior manipulation and entirely experimentally.

I see a few methods of getting more satisfying results and most of them involve manipulating the data to narrow the view of the training model.
- Limiting the data to one character (Cartman, for example)
- Removing non-major characters lines
- Removing songs, non-english words, and emotive phrasing in the data. (i.e "But mommmm!")

With more research into making my own RNN for this type of project, maybe I could gear one specifically to deal with the caveats of reading scripts with multiple characters.

Enjoy!

##Highlights

![alt text](https://github.com/deankeinan/SouthPark-rnn/blob/master/images/h1.png "Some sampled text")
*****
![alt text](https://github.com/deankeinan/SouthPark-rnn/blob/master/images/h2.png "Some sampled text")
*****
![alt text](https://github.com/deankeinan/SouthPark-rnn/blob/master/images/h3.png "Some sampled text")
*****
![alt text](https://github.com/deankeinan/SouthPark-rnn/blob/master/images/h4.png "Some sampled text")
*****
![alt text](https://github.com/deankeinan/SouthPark-rnn/blob/master/images/h5.png "Some sampled text")


And I'm sure there's more entertaining ones in there I haven't seen. 
