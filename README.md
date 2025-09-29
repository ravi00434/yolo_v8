YOLOv8 Traffic Cone Detection 
A very basic prototype for training, exporting, quantizing, and running inference with YOLOv8 to detect traffic cones for the self driving cars using Jupyter Notebook workflow 
Quick Start
1. Setup
Clone the repo and install dependencies:

bash
pip install ultralytics onnxruntime opencv-python matplotlib
2. Prepare Your Dataset
Use YOLO format (images + .txt annotations).

Update the data.yaml path in the notebook to point to your dataset.

3. Train the Model
Open yolov8.ipynb and run the training cell:

python
!yolo detect train \
  model=yolov8n.pt \
  data="/path/to/data.yaml" \
  epochs=50 \
  imgsz=640
Trained models and results are saved in runs/detect/.

4. Export and Inference
Export to ONNX:

python
from ultralytics import YOLO
model = YOLO('runs/detect/your_run/weights/best.pt')
model.export(format='onnx')
Quantize (optional, for speed):

python
from onnxruntime.quantization import quantize_dynamic, QuantType
quantize_dynamic('best.onnx', 'best_int8.onnx', weight_type=QuantType.QUInt8)
Run inference and visualize results:
See notebook cells for details on running ONNX inference and drawing bounding boxes.

Results
Example mAP50: 0.89 (YOLOv8n, 100 epochs)

See notebook for sample output images.
