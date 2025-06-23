# Building a Virtual Garment Try-On System

This document describes the basic steps to adapt **AnyDoor** for a clothing try-on application where users upload a person image and a garment image to preview the try-on result.

## 1. Prepare Data
- Collect product images of each garment and annotate segmentation masks.
- Optionally gather person images with ground truth segmentation.
- Update `configs/datasets.yaml` to point to your dataset paths. You can reuse the entries `VitonHD`, `Dresscode` or `FashionTryon` as examples.

## 2. Download Model Weights
- Download the pre-trained AnyDoor checkpoint and DINOv2 weight as described in `readme.md`.
- Edit `configs/anydoor.yaml` line 83 to set the path to the DINOv2 weight.
- Place the AnyDoor checkpoint path in `configs/tryon_demo.yaml`.

## 3. (Optional) Fine-tune on Your Dataset
- Adjust `run_train_anydoor.py` to include only your try-on datasets.
- Set training hyper-parameters (batch size, learning rate, etc.).
- Run `python run_train_anydoor.py` to start fine-tuning.

## 4. Run the Try-On Demo
- Check `configs/tryon_demo.yaml` and set the paths as above.
- Start the Gradio interface:

```bash
python run_tryon_demo.py
```

- Upload a person photo on the left and a garment image on the right. Draw rough masks on both images. Click **Generate** to preview the result.

## 5. Integration Tips
- Deploy the demo on a local server connected to a kiosk or a mobile front-end.
- You can pre-load your store's garment images in `examples/Gradio/FG` so they appear as selectable examples in the interface.
- For better quality, enable `Reference Mask Refine` to automatically refine the garment mask.

This setup provides a starting point to build an efficient and user-friendly virtual try-on system using AnyDoor.
