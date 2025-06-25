ComfyUI: Image-to-3D and Text-to-Image Workflow
This repository contains a powerful and versatile ComfyUI workflow that combines two distinct functionalities: generating a 3D model from a single 2D image and a separate, high-quality text-to-image generation pipeline.

This workflow is perfect for artists, designers, and enthusiasts who want to bring their 2D concepts to life in 3D or generate stunning images from text prompts.

✨ Key Features
Image-to-3D Conversion: Transform a 2D image of an object into a 3D mesh (.glb file).
Automatic Background Removal: Intelligently isolates the subject from its background to create a clean mask for 3D generation.
High-Quality 3D Generation: Utilizes the Hunyuan3D model for robust mesh generation.
Integrated 3D Preview: View the generated 3D model directly within the ComfyUI interface.
Separate Text-to-Image Pipeline: Includes a complete JuggernautXL based workflow for generating high-resolution images from text prompts.
Organized & Grouped: The workflow is neatly organized into logical groups for clarity and ease of use.
🖼️ Workflow Visualization
(It is highly recommended to add a screenshot of your ComfyUI workflow here. It provides an excellent visual reference for users.)

⚙️ Setup & Installation
Before you begin, ensure you have a working installation of ComfyUI.

1. Install Custom Nodes
The easiest way to install the required custom nodes is with the ComfyUI Manager.

Use the "Install Custom Nodes" feature in the manager to search for and install the following:

ComfyUI Essentials (for background removal and image resizing)
Git Repo: https://github.com/cubiq/ComfyUI_essentials
ComfyUI Hunyuan3D Wrapper (for the core 3D generation)
Git Repo: https://github.com/kijaidesign/ComfyUI-Hunyuan3DWrapper
2. Download Required Models
Place the following models into the correct directories within your ComfyUI/models/ folder.

Hunyuan3D Model:

File: hunyuan3d-dit-v2-0-fp16.safetensors
Download from: Hugging Face
Placement: ComfyUI/models/checkpoints/
JuggernautXL (for Text-to-Image):

File: juggernautXL_ragnarokBy.safetensors (or any other SDXL checkpoint of your choice)
Placement: ComfyUI/models/checkpoints/
After installing all nodes and models, restart ComfyUI.

🚀 How to Use
Load the Workflow: Drag and drop the image and text to 3d.json file onto the ComfyUI window.

Image-to-3D Generation:

Locate the LoadImage node in the "Generate 3D Model from Image" group.
Click "Choose file to upload" and select the 2D image you want to convert. The image will be automatically resized and its background removed.
Queue the prompt. The final .glb file will be saved in the ComfyUI/output/3D/Hy3D/ directory, as specified in the Hy3DExportMesh node.
Text-to-Image Generation:

This part of the workflow is separate and can be run independently.
Locate the two CLIPTextEncode nodes in the far-left group.
Enter your desired "positive prompt" in the top node and your "negative prompt" in the bottom node.
Queue the prompt. The resulting image will be saved in your standard ComfyUI/output/ directory.
workflow Sections Explained
This workflow is divided into two main, independent groups.

Image-to-3D Conversion
This is the core of the workflow. It follows these steps:

Load & Prepare: The input image is loaded, resized to the optimal 518x518 resolution for the model, and a mask is created by removing the background.
Generate Mesh: The prepared image and mask are passed to the Hy3DGenerateMesh node, which creates a latent representation of the 3D model.
Decode & Refine: The latent is decoded into a triangle mesh (trimesh) by the Hy3DVAEDecode node and then cleaned up by the Hy3DPostprocessMesh node.
Export & Preview: The final mesh is exported as a .glb file and can be viewed in the Preview3D node.
Text-to-Image Generation
This is a standard, high-quality text-to-image pipeline that uses the loaded SDXL checkpoint (JuggernautXL by default) to generate images based on your text prompts.

⚠️ Notes & Troubleshooting
The image encoder for the 3D model works best with 518x518 images. The workflow handles this resizing automatically, but starting with a clean, centered subject will yield the best results.
If the Preview3D node appears broken or fails to load, right-click on it and select "fix node" or re-create it by adding a new Preview3D node. This can happen if your ComfyUI core has been updated since the workflow was created.
License
This workflow is released under the MIT License. Feel free to use, modify, and distribute it as you see fit.
