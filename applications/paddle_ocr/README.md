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