# C++ Face and eye Detector

This tutorial is for the person who hasn’t a clue about C++ and wants to get something as sophisticated as face recognition working. 
On the surface it would seem a difficult task given we are involving OPENCV, an open source library, as well the C++ application which must be compiled. But is it that hard? lets see, follow on.

## Requirements and Dependencies

Firstly you will need to install OPENCV on Mac OSX, Ubuntu or your Raspberry Pi or even Windows. Installing OPENCV can be a big ask for a novice. There are many great tutorials online for installation of OPENCV like…

here for raspberry pi https://www.pyimagesearch.com/2016/04/18/install-guide-raspberry-pi-3-raspbian-jessie-opencv-3/

here for Mac OSX https://www.pyimagesearch.com/2016/12/05/macos-install-opencv-3-and-python-3-5/

here for ubuntu https://www.pyimagesearch.com/2016/10/24/ubuntu-16-04-how-to-install-opencv/

or opencv.org itself such as https://docs.opencv.org/3.4.0/df/d65/tutorial_table_of_content_introduction.html where you can find installation instructions for any IDE or OS.

A note installing OPENCV on the Raspberry pi, it can take 8 hours to install! It has not gone to sleep! it just takes a really really long time to install because the raspberry pi is just so resource constrained!

Once you have OPENCV installed it should have created an ‘opencv’ folder in your home directory. For example on raspbian its /home/pi/opencv or mac OSX /User/yourname/opencv

Of course if you used a virtual environment you will need to locate the opencv path first. 
Some facts first about my set-up. I have OPENCV installed on Mac OSX, Raspberry pi ‘raspian jessie, and Ubuntu 16.04. All versions work with python 3.6 and in the case of raspbian, python 3.4.

But this tutorial is about C++. It does not matter with OPENCV as to either language Python or C++, as it has two code interfaces, primarily though C++ with a Python wrapper for using Python but natively its really a C++ application.
You should have Cmake installed, it is probably installed on OSX at least it was on mine, it certainly is on Raspbian and also Ubuntu. If not please install Cmake. I will use Cmake as the terminal not GUI.

What if you have OPENCV already installed but don’t know the version? At the terminal prompt type:

pkg-config --modversion opencv

So assuming you have OPENCV installed e.g.. OPENCV 3.3.1 for example, (though this worked on 3.2 as well or earlier versions) we are ready to start.

## Instructions

I will walk through the tutorial  so you can get a better feel what came first rather than blindly copy and paste a few links.

Step 1. in your home directory such as /home/pi/  go to the opencv folder. e.g. home/pi/opencv

Step 2. type: mkdir face ( so now you will have  a directory structure of /home/pi/opencv/face) then type: cd face

Step 3. You should be in the face directory. Lets grab the source code from the web. Open a web Browser and goto https://opencv.org

Step 4. on the top line of the home page find ‘RELEASES’ and click

Step 5. then scroll down and choose 3.3.1 documentation ( you can choose 3.4 or later if you have that)

Step 6.  under ‘OpenCV Tutorials’ choose ‘Object Detection’ so you should be here : https://docs.opencv.org/3.3.1/d2/d64/tutorial_table_of_content_objdetect.html

Step 7.  next choose ‘Cascade Classifier’ which should be here:  https://docs.opencv.org/3.3.1/db/d28/tutorial_cascade_classifier.html

Step 8. Time to code. copy all the C++ code in the box using ctrl-c or copy.

Step 9.  Go back to your terminal (Command Prompt) make sure you are in the folder you created called ‘face’ which on the raspberry pi is /home/pi/opencv/face

Step 10. type: nano

Step 11. ctrl-v or paste (which should dump the code you copied into the nano editor)

Step 12. ctrl-x then y then <enter>

Step 13. Next we must make the CmakeLists.txt file, to do that, in the web browser jump to https://docs.opencv.org/3.3.1/db/df5/tutorial_linux_gcc_cmake.html

Step 14. go down to ‘Create a Make file’ and copy the box.

Step 15. (inside your face directory type) type: nano CMakeLists.txt

Step 16. copy the code.

Step 17. now change every entry that has ‘DisplayImage’ to ‘face’ so it should look like….

cmake_minimum_required(VERSION 2.8)
project( face )
find_package( OpenCV REQUIRED )
include_directories( ${OpenCV_INCLUDE_DIRS} )
add_executable( face face.cpp )
target_link_libraries( face ${OpenCV_LIBS} )

Step 18. ctrl-x, y, <enter>

Step 19.type:  cmake . 

Step 20. type: make

Step 21. type: ./face

Step 22. Its likely you will get an error that will say ‘--(!)Error loading face cascade’ it means it cannot find the Haars cascades xml files. No problem. if so proceed to Step 23.

Step 23. type: nano face.cpp

Step 24. remove the extra ../ so you have only {face_cascade|../data/haarcascades/haarcascade_frontalface_alt.xml|} and {eyes_cascade|../data/haarcascades/haarcascade_eye_tree_eyeglasses.xml|}")

Step 25. ctrl-x, y, <enter>

Step 26. cmake .

step 27. make

## Conclusions

Its all too easy. No fancy IDE, no project folder tree. Sure I could have condensed it by putting links straight from GitHub, but this way you can ‘twist the plot’ to suit your arrangement. The source files are included for the raspberry pi in this repository.

So you should on a Mac, or if you have a usb camera on your raspberry pi, see your face in a circle with your eye’s circled as per the images at  https://docs.opencv.org/3.3.1/db/d28/tutorial_cascade_classifier.html

The good thing is that it works well on the raspberry pi as it does on Mac OSX which unlike machine learning solutions which will be exceptionally slow on the raspberry pi (usually). But of course haar cascades just won’t have the accuracy of a well trained machine learning classifier.

FYI: Windows will require more work as the paths are different for a start to the hard cascade xml files. You may encounter other issues as the commands here are for OSX or Debian like linux.

