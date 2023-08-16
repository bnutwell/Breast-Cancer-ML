# AIplus-Practicum-Final
Final deliverable package for AI+ Practicum Team 1 - Summer 2023

    Tyler J Lang, Brian Nutwell, Frank (Feng) Wen

To use the notebooks provided, data must be moved to the Data folder provided. Please see individual notebooks for any requirements regarding location references or structure of data, depending on if the data being presented is being used to fine-tune a model, or use a pre-trained model to predict on a set of data. 

_________________________________________________________
Diagnosing New Images:

Best results were obtained by first cropping images to show only the ultrasound picture data (removing text and other border artifacts from the images). See the notebook \data_preprocessing\image_cropping_AIplus.ipynb for example of how to do this.  Place the images and labels in subfolders under \Data\ and update the notebook paths accordingly.

"AIplus_1step_pipeline.ipynb" is our current, best-performing notebook for predicting new images, and will perform all steps associated with object detection, including providing the coordinates to crop the tumor from the image, and predict the type of tumor as benign or malignant. Please see notebook-specific instructions for help on running the notebook.  This notebook expects a single trained YOLOv8 model: 'best_yolo_1step.pt' is our proposed model.

"AIplus_2step_pipeline.ipynb" uses YOLOv8 for segmentation and DenseNet for classification, but performance is inferior to the 1-step model.  Image preparation is similar to above, and 2 trained models must be specified of course.  This notebook requires the 'AIplus_Utilities.py' file to be in the same folder.

_________________________________________________________
Training Models:

To train YOLO models, the labels must be converted to YOLO .txt file format, and the data + labels must be placed in \imgs\ and \labels\ subfolders respectively.  These notebooks are in the \data_preprocessing\ subfolder.

Notebook 'yolo_format_convert.ipynb' has the code to do this.  "Single class" conversion blocks create labels of type 'tumor' for segmentation only, while "Multiclass" conversion blocks create labels for the 1-step model training.

Notebooks 'data_preprocess_BUSI.ipynb' and '..._OASBUD.ipynb' are similar, but for externally sourced datasets.

After images are preprocessed, the following training notebooks can be used:
- 'yolov8_multiclass_train.ipynb' is our best-performing approach, to create the 1-step model
- 'yolov8_segment_train.ipynb' will create a segmentation only model for the 2-step approach
- 'densenet_class_train.ipynb' will create a classification only model for the 2-step approach

Note that YOLO notebooks specify an accompanying .yaml file, which must also be present, and which must contain correct path links to the training & validation data.

_________________________________________________________
Deprecated Content:

Within the "Deprecated" folder, notebooks can be found regarding processess that we experimented with, and were ultimately outperformed by our current model architecture via the 1-step YOLO object detection model. Included processess include a notebook dedicated to post-cropped tumor classification (benign or malignant) using a variety of deep learning architectures and strategies, and is used to ultimately train a DeepNet model that, when provided croppped tumor images, can achieve accuracy of 85% on an unseen test set. It also includes our Faster-RCNN model previously used for object detection, which was then replaced by YOLO, but is mentioned in our final report. "aiplus_baseline" contains various experiments ran on different formats of the YOLO model, to find the best model to use in the 1-step pipeline. 

_________________________________________________________
Final Report:

A formal report of findings can be found in "Final Report.pdf"

----------------------------------------------------------------------