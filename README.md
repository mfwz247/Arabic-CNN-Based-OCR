# Arabic-CNN-Based-OCR
object detection based


Good morning! This is Mohamed Fawzy.

For the stubborn case of arabic handwritten words recognition which is so hard due to the hierearchy of the word itself...

Arabic words are written continously without pauses unlike English words! 

![image](https://user-images.githubusercontent.com/81578056/159821666-11db0476-2c11-4531-95aa-0dec2c63e894.png)

But English words:

![image](https://user-images.githubusercontent.com/81578056/159821741-ac5196b9-17d0-4019-8701-d614fb2c5647.png)

Another problem is that every single character has three forms/shapes

How I tried to solve this out:

## First Apporach: OpenCV find/draw contours

The most popular approach to acheive characters recognition which is by finding contours using OpenCV doesn't work for arabic words!

Why?? Because contouring a single character is not possible as every character is connected with its neighbors.

![marked areas](https://user-images.githubusercontent.com/81578056/159823706-c43b7ca0-709e-4761-a0b7-f78e1a8c4bbd.jpeg)

While in English: 

![image](https://user-images.githubusercontent.com/81578056/159824247-0c828726-deda-40ed-a20c-d0d143a24a47.png)

## Second Approach: Training on words that an actual OCR had recognized succesfully.

This approach is kinda limited as Arabic has 12.3 Million words.

I trained a VGG16 model with input of handwritten augmented words and their labels using AlexU dataset that contains 109 unique words.

![67-3](https://user-images.githubusercontent.com/81578056/159824781-f1dbc3af-42e0-42bb-8453-bba4e33dc0ec.jpg)

with 85% of validation accuracy.

## Third Approach: Using already sliced characters dataset

which I found here https://github.com/HusseinYoussef/Arabic-OCR

Thanks to Eng. Hussein Osama!

here's a sample of ب : 

![0](https://user-images.githubusercontent.com/81578056/159825991-bc530a34-13b8-422d-adde-85514e643a4e.png)
![4](https://user-images.githubusercontent.com/81578056/159825994-c8af53a9-684b-42ea-9d88-59efba4780c4.png)
![13](https://user-images.githubusercontent.com/81578056/159825996-7ea5260b-1a9a-4121-bd63-26ff4c8166e9.png)

I also thought of splitting the image to vertical rectangles where every rectangle may contain a character.

![sliding_window_example](https://user-images.githubusercontent.com/81578056/159825733-5fc486e0-299e-4637-aae0-0dc88c1b71e3.gif)



So to implement it i used the code here: https://pyimagesearch.com/2020/06/22/turning-any-cnn-image-classifier-into-an-object-detector-with-keras-tensorflow-and-opencv/

which splits the image into ROI's (Region of interests) and search for the characters.

## Fourth Approach: Mimicing an actual OCR (Reinforcement Learning)

we can actually make an ocr that already works perfectly with arabic to giveback its results to the model for every batch!

this way we don't have to worry about tuning deep nets.

reinforcement learning is dynamically learning by adjusting actions based on continuous feedback to maximize a reward.

It will just take ages to train it.
