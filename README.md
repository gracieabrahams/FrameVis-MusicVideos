# FrameVis-MusicVideos

Gracie Abrahams & Eva Wallis

**Introduction:**
For this project, we wanted to explore image processing and manipulation tactics that we have done with images throughout the semester with videos. 
With this, we set out on a goal to read in movie mp4 files and manipulate the frames in different ways to learn about the coloring and object patterns within them. 
We came across a Github project called FrameVis, which generates “movie barcodes,” which takes frames from a video file at a regular interval, resized, and then stacked together to show the compressed color palette of the video and how it changes over time. 
Here we take different frames and convolve them with blur and sobel detection filters.  Using the starter code provided from Github, we were able to generate mp4 barcodes. 
We initially began with the idea of recreating these movie barcodes, with the added goal of exploring the meaning behind the color schematics of the movie. 
We started with large movie files, but after we started to modify and test our code, we quickly realized it would be more time efficient to practice with shorter clips. 
From this, we resorted to music videos. There are plenty of different ways we thought we could analyze these videos, comparing black and white videos to color videos, comparing recurring objects within videos through object detection, and putting the frames all together to find patterns and their implications within the total video. 

**Our Code/Functions:**
The function generate_barcode() is the main function used in the program, which takes 4 parameters: the source of the video, the number of frames requested for the barcode, and 2 boolean flags, blur and average, that are used later to determine the type of barcode being generated.
We used the several built-in video functions within the cv2 library for importing the videos, splitting them into frames, and getting size info from the files. The program uses the inputted number of frames to determine which frames within the video to select. It automatically will space the chosen frames evenly throughout the video.
If the user were to select only 1 frame, it would be the scene halfway through the film or video. It iterates through these selected frames, and depending on the boolean flags that were set, blurs the image or calls the average function. The blur was a built-in Gaussian blur function from cv2, using an 11x11 kernel. The average function briefly shrinks the image to only 1 pixel tall while maintaining its original width, before resizing it again to its original dimensions.
This essentially takes the average color through each vertical column of the image. The below image displays 1 frame from Alice in Wonderland, against the average of that same frame. You can clearly see where each color average comes from within the original image.
After blurring or averaging the image, the program shrinks the image to a predetermined width, and horizontally concatenates them together in an output image, thus creating the barcode. This function is adapted from FrameVis and contains mostly source code, with some modifications.
Using generate_barcode(), we get a frame(s) of images that are measured on the x-axis by time. The x-axis is in percentages, so the .5 mark measures the frame that is at the halfway point of the video. To be able to generate a frame from any timestamp, we implemented 3 functions: find_timestamp(x_axis, length), timestamp_to_minutes(timestamp), and print_timestamp(source, timestamp_minutes). These functions allow the user to put in the percentage on the x-axis where they want to see a specific frame and find out what timestamp to look at by converting seconds to minutes and back. The timestamp is passed to the print_timestamp function, which will generate the frame at a specific time. We tested this and checked back with the actual music videos to ensure accuracy.
	Lastly, we implemented a generate_edge_detection() function to generate an edge detection of multiple frames in the video using convolution with the built in Sobel detector (3x3 kernel). This helps us identify important objects and images within these videos, especially if there is a busy image with a lot of colors. There is a for loop, that makes sure however many images the user wants (we defaulted to 5), are printed out with the corresponding sobel detection.

**Implementation/Testing:**
For this program, we initially intended to work with films, but upon struggling with large file types and excessive runtime, we decided to work primarily with music videos. We gathered barcodes for the film Alice in Wonderland, as well as music videos for “Ripple” by the Grateful Dead, and “Help!” by The Beatles. “Help!” is a black and white video, while “Ripple” contains various bright colors and objects. For each video, we wanted to generate a barcode of 5 frames, 500 frames, and 1000 frames. With this, we can visualize the overall video, and look into patterns in coloring, brightness, and the overall feel of the video. For example, with the Grateful Dead video, an array of colorful bright images would signal that this may be a more upbeat, exciting video/song. We additionally experimented with the output of the barcodes by using a blur filter and applying an average function. Each gives a slightly different look, but the average functions show the cleanest display of color schematics. 
Next, we try to detect objects within different frames of the videos using a sobel filter. We apply this to all of the individual frames we generate to see what different objects/edges may be important in the video.
After generating the barcode, we were intrigued to see what a single frame would look like based on the combination of colors in the middle towards the 0.5 mark on the x-axis, which represents 50% of the way through the music video. Given the music video had a length of 4:24, our 50% mark would be 2:12, which we run through a function to convert into minutes (2:12 ~ 2.2 minutes). We pull the 2.2 minute mark using our print_timestamp() function and see those blue and purple colors from the barcode as a full frame above.
Next, we visualized multiple frames from throughout the video and compared their sobel edge detections.Through sobel edge detection, we were able to understand more about the music video and its 
eccentric graphics, and see some main themes/objects within the video. Especially when there are so many colors in the video, the edge detection allowed us to really narrow in on the exact objects within the video. To test our code further, we thought we should try this with a video that was in Black and White. Given this, we used the music video “Help!” by the Beatles. These results reveal less to us since the video is in black and white. However, we were interested in the sobel detection and how that may identify the band members in this more relaxed video. 
Band members are detected using the sobel filter, although it is not as crowded of an image as the Grateful Dead. Even though the video is in black and white, the barcode and sobel detections allow us to see that there is not much movement or change of scenery throughout the video, showing us that the song may not be as intense as Ripple, which holds true to the Beatles’ sound.

**Conclusion:**
Throughout this project, we were able to apply much of our knowledge of image processing/convolution to videos, which was very interesting to learn about and interact with through the FrameVis framework. We were able to take the starter code, and implement strategies that we have used in previous homeworks to make assessments about the video data we looked at and understand how colors, and objects played a role in each of the videos. We tested our data with different frame sizes, different variations of colors within the video, and different styles of videos. We were able to see that video size played a huge role in what we were able to accomplish, as we came in with a goal of interpreting full movie frames, but we needed to optimize time when testing. In the future, we would still like to explore these ideas further with movies. 
	
References:

Github:
​​https://github.com/dmadison/FrameVis/tree/master?tab=readme-ov-file

Starter Code:
https://www.partsnotincluded.com/framevis-video-visualizer/

Journal Referenced:
http://www.sciresit.it/article/view/13606/11993 





