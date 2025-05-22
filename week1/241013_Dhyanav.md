First of all, I imported the picture and made it grayscale.

Then, I tried to code Canny edge filter. After some debugging, some using article and some using LLMs, I was able to make it work.
Experiments I did:
1.) With sigma in Gaussian filter. I experimented with values around 2 and finally stuck to 2.
2.) In double threshold, initially I used 0.05 and 0.15 as thresholds but then realised that I got better results with lower values. So, I decided to use 0.02 and 0.04 finally.

Besides, I also implemented Sobel filter. After experimenting, I stuck with threshold = 0.3

I also tried implementing Scharr filter.
