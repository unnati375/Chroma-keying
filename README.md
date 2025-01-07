# Chroma-keying (Statistics Project)
Removing the green screen background keeping the foreground unchanged <br /> 

In these codes we are only showing our implementation using the "image2.png" because it is the most critical image to process as per our concern, But our algorithm also works well for other images also. So these algorithm can be applied over all the images, those we have used so far. We just have to change the image name every time in order to apply these algorithm for different images. <br /> 
## Different approaches 
### Histogram screening
We observe from the histograms of most of  our images that some collected bars are very high and the rest are very low compared to them and the height abruptly reduces at a certain point. The background will have relatively high values of green component and the variation  will be lower as well, so the abruptly elevated bars represent the points in background. We can then estimate the particular range for the three components by looking at the histogram , and remove all the points with color components in that particular range.

### A Slightly smarter approach 
Our previous approach doesn't account for the fact that in the background the green component will be higher and the red and blue components will be lower. So we give an upper bound for the red and blue component along with the lower bound for the green component. Using this fact we can give a smarter bound for example red and blue component < 0.5 and green component > 0.35 works pretty well.
### A different implementation 
Instead of taking  bounds for red, blue and green components why don't we bound the ratios g/r and g/b , we can say they will be surely more than 1 for the background as it is green and by observation we have found out that if g/r and g/b values are greater than 1.2(call it the super bound) then, it works quite well. Also, we have noticed that we get the best possible images by varying the super bound between 1 and 2 , that means we check each image for super bounds in {1,1.1,1.2,...,2} .We also get 1.2 as the super bound most of the time. Start implementing with 1.2, if excess foreground is removed , a value greater than 1.2 works and if green background is left behind(very rare case for our sample), a value less than 1.2 works.
 ### The super bound approach 
 Our algorithm predicts that points whose g/r and g/b value > super bound is in background. Now if we take our blank green screen and find the min of g/r values , it would be 1.289340 , similarly the min of g/b values would be 1.231884. Now we will take 90 percent (1.160406, 1.1086956 (call it b-bound)) of these to account for slight changes to the background owing to the fore ground. After applying these bounds to our pictures, all points in our background should be removed at the cost of some of our foreground (like in Adeesh's image, Mayank's image, wherever the observed super bound is greater than 1.1086956). The minimum ratio does not change much because any change that the foreground brings to the background is percentage change in the three components that cancels out when we take the ratio. 
            








