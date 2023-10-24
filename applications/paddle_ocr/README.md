# PaddleOCR Application

## set environment

cd ./applications/paddle_ocr
git clone -b release/2.7 https://github.com/PaddlePaddle/PaddleOCR.git
pip3 install -r requirements.txt
cd ../..

## Download the weights

```
wget -nc -P ./applications/paddle_ocr/weights https://paddleocr.bj.bcebos.com/PP-OCRv4/chinese/ch_PP-OCRv4_det_infer.tar
cd ./applications/paddle_ocr/weights && tar xf ch_PP-OCRv4_det_infer.tar && cd ../../..

wget -nc  -P ./applications/paddle_ocr/weights https://paddleocr.bj.bcebos.com/PP-OCRv4/english/en_PP-OCRv4_rec_infer.tar
cd ./applications/paddle_ocr/weights && tar xf en_PP-OCRv4_rec_infer.tar && cd ../../..

wget -nc  -P ./applications/paddle_ocr/weights https://paddleocr.bj.bcebos.com/dygraph_v2.0/ch/ch_ppocr_mobile_v2.0_cls_infer.tar
cd ./applications/paddle_ocr/weights && tar xf ch_ppocr_mobile_v2.0_cls_infer.tar && cd ../../..

rm -rf ./applications/paddle_ocr/weights/*.tar

```

## Run convert paddle to ONNX:

```

paddle2onnx --model_dir ./applications/paddle_ocr/weights/ch_PP-OCRv4_det_infer \
--model_filename inference.pdmodel \
--params_filename inference.pdiparams \
--save_file ./applications/paddle_ocr/weights/det_onnx/model.onnx \
--opset_version 11 \
--input_shape_dict="{'x':[-1,3,-1,-1]}" \
--enable_onnx_checker True


paddle2onnx --model_dir ./applications/paddle_ocr/weights/en_PP-OCRv4_rec_infer \
--model_filename inference.pdmodel \
--params_filename inference.pdiparams \
--save_file ./applications/paddle_ocr/weights/rec_onnx/model.onnx \
--opset_version 11 \
--input_shape_dict="{'x':[-1,3,-1,-1]}" \
--enable_onnx_checker True


paddle2onnx --model_dir ./applications/paddle_ocr/weights/ch_ppocr_mobile_v2.0_cls_infer \
--model_filename inference.pdmodel \
--params_filename inference.pdiparams \
--save_file ./applications/paddle_ocr/weights/cls_onnx/model.onnx \
--opset_version 11 \
--input_shape_dict="{'x':[-1,3,-1,-1]}" \
--enable_onnx_checker True

```


## Test prediction via ONNX

```
cd ./applications/paddle_ocr/PaddleOCR/
python tools/infer/predict_system.py --use_gpu=False --use_onnx=True \
--det_model_dir=../../paddle_ocr/weights/det_onnx/model.onnx  \
--rec_model_dir=../../paddle_ocr/weights/rec_onnx/model.onnx  \
--cls_model_dir=../../paddle_ocr/weights/cls_onnx/model.onnx  \
--image_dir=doc/imgs_en/img_12.jpg \
--rec_char_dict_path=ppocr/utils/en_dict.txt
```