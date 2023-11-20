# Convert-Image-To-Pdf
Effortlessly transform images into PDFs with Python, simplifying document management and organization.

from reportlab.pdfgen import canvas
from PIL import Image

def convert_images_to_pdf(image_paths, output_pdf):
    c = canvas.Canvas(output_pdf)
    pdf_width = 595.276  # PDF standard width
    pdf_height = 841.890  # PDF standard height
    c.setPageSize((pdf_width, pdf_height))
    image_width = pdf_width / 2
    image_height = pdf_height
    gap = 10  # Adjust as needed
    total_width = 2 * image_width + gap
    x_offset = (pdf_width - total_width) / 2
    for i, image_path in enumerate(image_paths):
        print(f"Attempting to open image: {image_path}")
        try:
            img = Image.open(image_path)
            y_offset = (pdf_height - image_height) / 2
            x_offset += i * (image_width + gap)
            c.drawInlineImage(img, x_offset, y_offset, width=image_width, height=image_height)
        except Exception as e:
            print(f"Error opening image {image_path}: {e}")
    c.save()
if __name__ == "__main__":
    image_paths = ["paste your image path.jpg", "paste your image path.jpg"]
    output_pdf = "output.pdf"
    convert_images_to_pdf(image_paths, output_pdf)

    print(f"PDF created successfully: {output_pdf}")
