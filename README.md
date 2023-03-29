# Newspaper-Segmentation-using-YOLO

YOLOv3 is extremely fast and accurate. In mAP measured at .5 IOU YOLOv3 is on par with Focal Loss but about 4x faster. Moreover, you can easily tradeoff between speed and accuracy simply by changing the size of the model, no retraining required!

First of all I needed a dataset of labelled images to train the Yolo model and there were none available so I decided to make my own.
After hours of mouse pointing and drawing bounding boxed and manually labelling newspaper images I ended up with a 32 image dataset with 4 classes

Headline,
Logo,
Image,
Text.



Now, even though we’re training our model on a custom dataset, it is still advantageous to use another already trained model’s weights as a starting point. Think of this like we want to climb a mountain as quickly as possible, and instead of starting completely from scratch in creating our own trail, we’ll start with assuming that someone else’s trail is a better faster than us randomly trying to guess twists and turns to follow.

To power our model’s computation, we’ll be using Google Colab, which provides free GPU compute resources (up to 24 hours with your browser open).

Started off by cloning Joseph Redmond’s Github repo. This provides most of the tools required to train object detection models on the fly.


git clone https://github.com/pjreddie/darknet


Edit the yolo-v3.cfg file to configure it according to your requirements

You need to put your no. of classes in the first line, train.txt and test.txt path in 2nd and 3rd line, object.names path in the 4th line.

Now you need to edit the *.cfg file. By default each YOLO layer has 255 outputs: 85 outputs per anchor [4 box coordinates + 1 object confidence + 80 class confidences], times 3 anchors.

In our case we are using only four classes, then we need to edit the filter. You can reduce filters to filters=[4 + 1 + n] * 3, where n is your class count. This modification should be made to the layer preceding each of the 3 YOLO layers. Also, modify classes=80 to classes=n in each YOLO layer, where n is your class count.

I changed the batch size & subdivisions which is in line no. 6 and 7. Then line no 610 (classes=4) and 603 (filters=27), then line no. 689 & 696, lastly line no. 776 & 783.





