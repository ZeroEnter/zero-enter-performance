# PaddleOCR Application

## Download the weights

```
wget -nc -P ./applications/paddle_ocr/weights https://paddleocr.bj.bcebos.com/PP-OCRv4/chinese/ch_PP-OCRv4_det_infer.tar
cd ./applications/paddle_ocr/weights && tar xf ch_PP-OCRv4_det_infer.tar && cd ../../..

wget -nc  -P ./applications/paddle_ocr/weights https://paddleocr.bj.bcebos.com/PP-OCRv4/chinese/ch_PP-OCRv4_rec_infer.tar
cd ./applications/paddle_ocr/weights && tar xf ch_PP-OCRv4_rec_infer.tar && cd ../../..

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


paddle2onnx --model_dir ./applications/paddle_ocr/weights/ch_PP-OCRv4_rec_infer \
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