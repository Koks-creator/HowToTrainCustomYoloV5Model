# How to train custom YoloV5 model using ultralytics

<h2>1. Prepare data</h2>
<ul>
  <li>Requirements:</li>
  <ul>
    <li>labelimg (https://pypi.org/project/labelImg/)</li>
    <li>Download All Images browser extension (or any other image downloading extension)</li>
  </ul>
  <li>Steps:</li>
  <ul>
    <li>Download images.</li>
    <li>Unpack them, delete non png/jpg files.</li>
    <li>Prepare train data folder structure:</li>
    
![Screenshot_8](https://github.com/Koks-creator/HowToTrainCustomYoloV5Model/assets/73878161/0ccd0b77-abd0-4353-b798-19cac6e728a8)

  <li>Run labelimg - type: labelimg in terminal.</li>
  <li>Open dir with images, set "save dir", set output file type to "YOLO".</li>

  ![Screenshot_9](https://github.com/Koks-creator/HowToTrainCustomYoloV5Model/assets/73878161/9e6ef5f1-45b9-4c45-844f-01d2dacf6341)

<li>Label by clicking "Create RectBox" and set label - do it for all of images, the more images the better./</li>
<li>Your classes will be stored in classes.txt file in output dir.</li>
<li>Once you're done, create zip file and upload it to yolov5 folder in homepage of google drive (create yolov5 folder if doesn't exist)./</li>
  </ul>
</ul>


<h2>2. Train</h2>

<ul>
  <li>Copy colab notebook: https://colab.research.google.com/github/ultralytics/yolov5/blob/master/tutorial.ipynb</li>
  <li>Turn on GPU in colab: execution environment -> change type of execution environment -> GPU.</li>
  <li>Add the following cells in "Train" section (after logging) to intergrate notebook with Google Drive: </li>
  <br>
  from google.colab import drive <br>
  drive.mount('/content/gdrive')<br>
  !ln -s /content/gdrive/My\ Drive/ /mydrive<br>
  !ls /mydrive<br>
  <br>
  !unzip /mydrive/yolov5/train_data.zip -d /content <br>
  <br>
  !cp /mydrive/yolov5/custom_data.yaml /content/yolov5/data

  <li>Run setup section.</li>
  <li>Download /content/yolov5/data/coco128.yaml and adjust it to your needs - see custom_data.yaml in this repo. Save it as custom_data.yaml and upload it to yolov5 folder on your google drive.</li>
  <li>Run cells you've added in colab notebook.</li>
  <li>Run last cell in "Train" section set: </li>
  <ul>
    <li>data: custom_data.yaml</li>
    <li>epochs: I suggest starting with 50, you can play around with it</li>
    <li>batch: play around with it, start with 16 or 32</li>
    <li>leave rest as is</li>
  </ul>
  <li>After training is done, you model will be stored in /runs/train/exp/weights in colab</li>
</ul>

<h2>3. Test</h2>
<ul>
  <li>Run 2nd cell in "Test" section, set: </li>
  <ul>
    <li>weights: path to model</li>
    <li>source: path to image</li>
  </ul>
  <li>Result will be stored in yolov5/runs/detect/ in colab</li>
  <li>You can display detection by adding cell: display.Image(filename='path to res image', width=600)</li>
</ul>

