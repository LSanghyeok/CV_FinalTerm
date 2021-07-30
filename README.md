AAA534-2021S: Final Project Proposal Lecture Note Generator![](Aspose.Words.9d04261a-3f63-48bb-a684-e111087c2a56.001.png)![](Aspose.Words.9d04261a-3f63-48bb-a684-e111087c2a56.002.png)

Sanghyeok Lee Minkyu Jeon

Abstract • Calculating homography for image registration from

each frame to our blackboard.

In this project, we aim to summarize the lecture

video. Given lecture video, we are able to convert • Extracting the contents of lecture that the instructor is it into lecture note with the computer vision tech- writing by using canny edge detector.

nology we learned in this semester. We achieve

our goals with image registration(RANSAC and • Removing instructor and noises with RANSAC and homography transformations), edge detection for ghost removal technique. extractingcharactersfromimages, ghostremovals

to remove instructor from video, and lecture note • Enhancing image with Kernel.

generation. We observe that proposed method is

na¨ıve but powerful for summarizing lecture. All

contents in this project started from scratch. • Clustering frames with the same content based on gra-

dient of color histogram and combine them in one slide.

\1. Introduction We will discuss the details of our method in Sec. [3.1 ](#_page1_x0.00_y609.65)and Nowadays, we can easily get online lecture videos through evaluate our method with qualitative analysis in Sec.[ 4](#_page2_x0.00_y654.01)

YouTube or the Internet. However, most of the lectures

offer videos without lecture note, and it is not easy to obtain 2. Dataset and Baselines

the lecture note for the corresponding videos. Although

most of the classes are replaced online due to COVID-19, 2.1. Dataset

some instructors(or professors) doesn’t provide the course To get the dataset for project, we download the lec- materials corresponding to the videos and they want us to ture video from YouTube : [https://www.youtube. ](https://www.youtube.com/watch?v=PRNy2ynqz2c)prepare for it ourselves. Especially in the case of outsiders [com/watch?v=PRNy2ynqz2c. According](https://www.youtube.com/watch?v=PRNy2ynqz2c) to the pur-

who are not registered in the lecture, the lecture note are pose of the project, we select a video that instructor often inaccessible even if they get the lecture videos. We records course that contents with hand written on the are motivated from this, we set our goal to develop an auto blackboard. Also this lecture video has less noise and lecture note generator from videos. screen conversion that may adversely affect the results. There are some approaches to extract contents from scenes. We also download the image of template blackboard For instance, OCR ([Smith,](#_page3_x0.00_y624.88) [2007)](#_page3_x0.00_y624.88) algorithm can detect the from here:[ https://www.crowdpic.net/photos/](https://www.crowdpic.net/photos/%EC%B4%88%EB%A1%9D%EC%B9%A0%ED%8C%90)

characters in each frames. However, since the style are [%EC%B4%88%EB%A1%9D%EC%B9%A0%ED%8C%90](https://www.crowdpic.net/photos/%EC%B4%88%EB%A1%9D%EC%B9%A0%ED%8C%90)We very different depending on each video, it cannot always firstsplit the video into image frames heuristically. We split guaranteethereasonableperformanceofOCR.Furthermore, the video to images every 2 seconds so the 34 min 20 sec even if the characters in each frame are detected perfectly, videos are separated in total 2,065 frames. We choose the the same strings could be repeated in the connected frames. front part as 300 frames(5 min) for simplicty and creating To handle the above issues, we need contents detector that the results.

guarantees the quality of the results with any videos and

time stamp detector to merge sections of the similar frames. 2.2. Baselines & SOTA

In this project, we propose a video-course material converter

that satisfies such needs. Our converter generates lecture We don’t have any baselines because we started this project notes summarizing the lecture based on the blackboard hand from scratch and we firsttry to implement it. So we show writing. The key process of our project of making converter our process in ablation study whether our proposed method are as follows: is work or not.

COSE362-2019F: Final Project Proposal![](Aspose.Words.9d04261a-3f63-48bb-a684-e111087c2a56.003.png)

![](Aspose.Words.9d04261a-3f63-48bb-a684-e111087c2a56.004.png)

Figure 1. Outline of our method. Each frame is processed to have only course content information through registration, edge detection, ghost removals and image enhancement, and finallywe summarize them to produce results.

\3. Method ![](Aspose.Words.9d04261a-3f63-48bb-a684-e111087c2a56.005.png)

All of our framework is composed of the computer vision techniques learned in AAA543 class including Random sample consensus(RANSAC ([Fischler & Bolles,](#_page3_x0.00_y489.39) [1981)),](#_page3_x0.00_y489.39) homography to remove the noise and get clear alignment result, and warping technology. We also use the canny edge detection to recognize the contents in the blackboard and ghost removal technique to remove the obstacles to the

blackboard. Figureframe,2.weFeaturfind featurese mappingand calculatefor imagemappingalignmentfunction. Fortoeachpre-

vious frame for image alignment.

1. Problem Definition

   2. Image Registration

Given a video which consits of frames fI1;I2;:::;Ing and

template imageI, our main objective is to generate a set of Lecture videos consists of a lot of frames. We extract frames images fI0;I0;:::;I0g that summarize the video on I(e.g., per 2 seconds as noted in [2.1 to](#_page0_x0.00_y431.62) generatefI1;I2;:::;Ing. At

1 2 k first, we should match the two images between the black-

blackboard, paper), where I is image and n is the last num-

ber of frame. board in lecture video Ii, and our template image I(e.g., front-view blackboard). But, converting each image Ii on

I is not a simple task. The view of the two images are

Figure 3. Image enhancing with kernel. ![](Aspose.Words.9d04261a-3f63-48bb-a684-e111087c2a56.006.png)![](Aspose.Words.9d04261a-3f63-48bb-a684-e111087c2a56.007.png)![](Aspose.Words.9d04261a-3f63-48bb-a684-e111087c2a56.008.png)

Figure 5. Color histogram of frames.![](Aspose.Words.9d04261a-3f63-48bb-a684-e111087c2a56.009.png)![](Aspose.Words.9d04261a-3f63-48bb-a684-e111087c2a56.010.png)

Figure 4. Ghost removal. Instructor block the blackboard(left) ![](Aspose.Words.9d04261a-3f63-48bb-a684-e111087c2a56.011.png)![](Aspose.Words.9d04261a-3f63-48bb-a684-e111087c2a56.012.png)![](Aspose.Words.9d04261a-3f63-48bb-a684-e111087c2a56.009.png)![](Aspose.Words.9d04261a-3f63-48bb-a684-e111087c2a56.010.png)and instructor is removed from the image(right). 

different, we need to apply image registration technique ![](Aspose.Words.9d04261a-3f63-48bb-a684-e111087c2a56.013.png)![](Aspose.Words.9d04261a-3f63-48bb-a684-e111087c2a56.014.png)such as feature extracting, key-point matching, and finding homography transformation for alignment. Additionally we use RANSAC to alleviate the outliers and some noises. Ba- sically we conduct image alignment by warping firstframeI to the template imageI. We set the coordinates of each im- ages and match those images with ORB(Oriented FAST and Figure 6. Result. The lecture video was summarized with four Rotated BRIEF) [(Rublee et al., 2011)](#_page3_x0.00_y569.09) features by OpenCV images.

framework. And then each current frame Ii is aligned to

the previous frameIi1, considering the frame dependency. few frames. Specifically, if the current image frame isIi, we We observed that this method generates reasonable result bring the frames Ii10;i9;:::;i2;i1, Ii+1;i+2;:::;i+9;i+10 because of the consistency for each frames. and we set the new frame as the median of those 20 frames.

So we get new edges that are deleted instructor version of

3. Extracting content contents.

From Section[ 3.2,](#_page1_x0.00_y626.67) we have transformed image that aligned 3.5. Color Histogram

between video image frames and a blackboard template.

For the purpose of extracting the contents of the lecture, we The key to summarize the lecture video is a clear informa- apply the canny edge detector to the lecture video frames tion from each frame and clustering of them. Until Sec- Ii(i 2 Rn). We get detected edge in the frame and it con- tion [3.4, ](#_page2_x0.00_y630.79)we tried to extract the clear class contents from the sists of contents that contains the lecture and the instructor. video. In this section, we will discuss the way to integrate At first, we make the edge line thick by applying 2D ker- the redundant information.

nel to catch the necessary information(i.e., hand writing We note that the color histogram is different frame by frame. contents in blackboard) more clearly. In Figure[ 3,](#_page2_x0.00_y129.89) we com- As shown in [5,](#_page2_x0.00_y152.10) the color histogram is largely varying fol- pare the two thickness of edges to represent content. We can lowing the change of the content over the lecture. Also, show that the right one is more clear. We only need contents, although the histogram changes slowly due to the depen- so we try to delete the instructor in the frame. Section [3.4](#_page2_x0.00_y630.79) dency of each frame, we noticed that the histogram changes will discuss more detail.[ ](#_page2_x0.00_y630.79)dramatically when the whole content in blackboard is erased

or the scene is changed. Therefore, we cluster the frame

4. Ghost removal based on the time stamp that has large gradient.

We remove obstacles including instructor by using Ghost 4. Result

removal method which is learned in class AAA543. In

lecture note, the instructor figureis undesirable object. So Figure 5 shows the results of our method. From the video we just delete that figureby ”Ghost removal” algorithm. It is lecture with instructor, we make the lecture note in flat the method that removes the moving object by median of a blackboard. We are going to show the additional project

results at presentation time through the demonstration video.

5. Limitation and future direction

We have 4 limitations of our method. First, this method only detect the edge so the figurecontents except for edges are not captured. If the instructor share figuresin lecture, our method could not catch it. In future work, we would detect the object is whether class content or not, we just copy and paste it in our lecture note. The second is the hand writing seems unstable. Even if we apply kernel to enhance the quality, it remains many things to do. The thrid one is speed. If the frame size is large, the speed of processing is slow. So we need to consider computational burden. Lastly, we can try to use deep learning to more accurate segmentation result instead of using edge detection.

6. Conclusion

In this project, we discuss the way to summarize the lecture video and generate the lecture notes. We observed that our method is effective to transform the video into the lecture note, although it has some limitations. We believe that our method is helpful for online classes and video lecture which are stimulated nowadays.

7. Roles of team members
- Sanghyeok Lee : Image alignment, registration and edge detection.
- Minkyu Jeon : Ghost removal and lecture note genera- tion.

References

Fischler, M. and Bolles, R. Random sample con-

sensus: A paradigm for model fitting with appli- cations to image analysis and automated cartogra- phy. Communications of the ACM, 24(6):381–395, 1981. URL[ /brokenurl#http://publication. wilsonwong.me/load.php?id=233282275.](/brokenurl# http://publication.wilsonwong.me/load.php?id=233282275)

Rublee, E., Rabaud, V., Konolige, K., and Bradski, G. Orb:

An efficient alternative to sift or surf. In 2011 Interna- tional conference on computer vision, pp. 2564–2571. Ieee, 2011.

Smith, R. An overview of the tesseract ocr engine. In

Proceedings of the Ninth International Conference on Document Analysis and Recognition - Volume 02, ICDAR ’07, pp. 629–633, USA, 2007. IEEE Computer Society. ISBN 0769528228.
