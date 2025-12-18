# LiteNeRF: Efficient View Synthesis for Synthetic and Real-World Scenes

LiteNeRF is a compact neural radiance field model designed for high-fidelity **novel view synthesis** from sparse 2D images. By representing 3D scenes as a continuous **5D neural radiance field**, LiteNeRF achieves state-of-the-art photorealism with a memory footprint of **only 5 MB** — nearly **3000× smaller** than traditional volumetric methods.

---

## Quickstart

### 1. Create Environment

```bash
conda env create -f environment.yml
conda activate nerf
```

### 2. Download Example Data

```bash
bash download_example_data.sh
```

### 3. Train and Monitor

```bash
# Train on the LLFF Fern scene
python run_nerf.py --config config_fern.txt

# Launch TensorBoard to monitor training
tensorboard --logdir=logs/summaries --port=6006
```

---

##  Key Features

* **Massive Compression**  
  Condenses complex 3D scene geometry into a **5 MB MLP**, offering a **3000× reduction** in storage compared to MPI or voxel-based representations.

* **Continuous 5D Representation**  
  Models scenes as a function:

  ( (x, y, z, \theta, \phi) \rightarrow (\sigma, RGB) )

* **High-Frequency Detail**  
  Uses **Fourier-based positional encoding** to overcome spectral bias and recover sharp edges and textures.

* **Hierarchical Sampling**  
  A **coarse-to-fine sampling strategy** focuses computation on visible surfaces rather than empty space.

* **Differentiable Rendering**  
  End-to-end **volume rendering** enables optimization via gradient descent using photometric reconstruction loss.

---

##  Experimental Results

LiteNeRF maintains strong structural fidelity across both synthetic and real-world datasets.

| Dataset    | Scene  | PSNR ↑ | SSIM ↑ | LPIPS ↓ |
| ---------- | ------ | ------ | ------ | ------- |
| Synthetic  | Lego   | 32.54  | 0.961  | 0.050   |
| Real-World | Orchid | 28.52  | 0.912  | 0.134   |
| Real-World | Fern   | 25.17  | 0.798  | 0.280   |
| Real-World | T-Rex  | 26.80  | 0.880  | 0.195   |

**Average PSNR:** **28.26 dB**

---

## Usage & Configuration

### Dependencies

* Python 3.x
* TensorFlow-GPU == 1.15
* NumPy
* Matplotlib
* Imageio
* ConfigArgParse
* ImageMagick *(required for LLFF data loading)*

---

### Supported Datasets

* **LLFF (Real-World)**  
  Use `--dataset_type llff` (e.g., *Fern*, *Orchid*)  
  Requires camera poses generated via **COLMAP** or `imgs2poses.py`

* **Blender (Synthetic)**  
  Use `--dataset_type blender` (e.g., *Lego*)

* **DeepVoxels**  
  Use `--dataset_type deepvoxels`

---

### Coordinate Convention

Camera poses follow the standard **OpenGL convention** using (3 \times 4) matrices:

* **X** → Right  \
* **Y** → Up  \
* **Z** → Backwards

---

##  Citation

```text
Sankar, S., & Prabakar, A.
LiteNeRF: Efficient View Synthesis for Synthetic and Real-World Scenes
via Compact Neural Radiance Fields.
New York University.
```

---

##  Notes

* This implementation is optimized for **research and educational use**.
* TensorFlow 1.15 is required for compatibility with the original NeRF codebase.
* Training times vary depending on GPU memory and dataset resolution.

---
 If you find this project useful, consider starring the repository!
