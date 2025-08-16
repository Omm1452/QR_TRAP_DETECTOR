# QR Trap Detector – Social Threat Identification Platform

This project provides a simple graphical application built with **Tkinter** and **Pillow (PIL)** that scans **QR codes** from images and analyzes the embedded URL to detect potentially malicious or suspicious content.

The main goal of this tool is to help users identify **social traps**, **phishing links**, or other dangerous URLs before they are opened in the browser.

---

## ⚙️ Features

- 🔍 Scan QR codes from image files (PNG, JPG, JPEG, BMP)
- ⚠️ Detect suspicious or malicious domains (configurable list)
- ✅ Ask for user confirmation before opening non-suspicious links
- 🖥 Simple and user-friendly **Tkinter** interface
- 📦 Uses **PIL** for image processing and **pyzbar** for QR decoding

---

## 🧠 How It Works

1. User clicks on **“Scan QR from Image”**.
2. The program opens an image file picker.
3. The QR code inside the image is decoded.
4. The decoded URL is checked against a **list of suspicious domains**.
5. The user is either:
   - Warned if the URL is suspicious; **or**
   - Asked if they want to open the link in their browser.

---

## 🛠 Requirements

| Package     | Install Command                    |
|-------------|-------------------------------------|
| Pillow      | `pip install pillow`                |
| pyzbar      | `pip install pyzbar`                |

> **Note**: On Linux, `zbar` may need to be installed separately:  
> `sudo apt install libzbar0`

---

## 🚀 Usage

```bash
python main.py




##🧾 Example Code


```import tkinter as tk
from tkinter import filedialog, messagebox
from PIL import Image
from pyzbar.pyzbar import decode
import webbrowser

# Example list of suspicious domains (expand as necessary)
SUSPICIOUS_DOMAINS = [
    "phishing-site.com",
    "malware-link.net",
    "trap-social.com"
]

def is_suspicious(url):
    for domain in SUSPICIOUS_DOMAINS:
        if domain in url:
            return True
    return False

def scan_qr_code_from_image(image_path):
    image = Image.open(image_path)
    decoded_objs = decode(image)
    for obj in decoded_objs:
        data = obj.data.decode("utf-8")
        return data
    return None

def open_image():
    file_path = filedialog.askopenfilename(
        filetypes=[("Image Files", "*.png;*.jpg;*.jpeg;*.bmp")]
    )
    if file_path:
        result = scan_qr_code_from_image(file_path)
        if result:
            if is_suspicious(result):
                messagebox.showwarning("Trap Detected", f"Suspicious or trap link detected!\n\n{result}")
            else:
                answer = messagebox.askyesno("QR Code Detected", f"Safe link detected:\n\n{result}\n\nDo you want to open it?")
                if answer:
                    webbrowser.open(result)
        else:
            messagebox.showinfo("No QR Code", "No QR code detected in the selected image.")

# Simple Tkinter GUI
root = tk.Tk()
root.title("Social Trap Detector QR Scanner")
root.geometry("350x200")

label = tk.Label(root, text="QR Trap Detector \n( WELCOME To MY QR Threat Identification Platfrom)\nCreating By Monoranjan Banik", font=("Arial", 16))
label.pack(pady=20)

scan_btn = tk.Button(root, text="Scan QR from Image", command=open_image, font=("Arial", 14))
scan_btn.pack(pady=20)

root.mainloop()


```

##👨‍💻 Author

Monoranjan Banik

If you like this project, don’t forget to ⭐️ the repository!


## 📌 TODO (Ideas for Future Improvement)

* Add ability to scan QR codes from webcam

* Connect to a real-time malware / phishing database API

* Export scan results to a CSV or log file

* Add dark mode for the GUI

