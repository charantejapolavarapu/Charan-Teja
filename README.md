import streamlit as st
from PIL import Image
import os

# --- Page Config ---
st.set_page_config(page_title="Image Gallery", layout="wide")

# --- Title ---
st.title("📸 Streamlit Image Gallery")

# --- Load Images from a Local Folder ---
IMAGE_DIR = "gallery_images"

# Ensure the folder exists
if not os.path.exists(IMAGE_DIR):
    os.makedirs(IMAGE_DIR)
    st.info(f"Put your images inside the `{IMAGE_DIR}` folder.")

# List of image file names
image_files = [f for f in os.listdir(IMAGE_DIR) if f.lower().endswith(('.png', '.jpg', '.jpeg', '.gif'))]

# --- Display Images in Grid Format ---
if image_files:
    cols = st.columns(3)
    for idx, image_file in enumerate(image_files):
        image_path = os.path.join(IMAGE_DIR, image_file)
        image = Image.open(image_path)
        with cols[idx % 3]:
            st.image(image, caption=image_file, use_column_width=True)
else:
    st.warning("No images found in the `gallery_images` folder.")
