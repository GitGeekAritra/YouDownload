import tkinter as tk
from tkinter import filedialog, messagebox
from pytube import YouTube


def download_video():
    url = url_entry.get()
    if not url:
        messagebox.showerror("Error", "Please enter a YouTube URL")
        return
    
    try:
        yt = YouTube(url)
        stream = yt.streams.get_highest_resolution()
        save_path = filedialog.askdirectory()
        
        if save_path:
            stream.download(save_path)
            messagebox.showinfo("Success", "Download Completed!")
        else:
            messagebox.showwarning("Warning", "Download canceled.")
    
    except Exception as e:
        messagebox.showerror("Error", f"Failed to download video: {e}")


root = tk.Tk()
root.title("YouTube Video Downloader")
root.geometry("400x250")

tk.Label(root, text="Enter YouTube URL:", font=("Arial", 12)).pack(pady=10)
url_entry = tk.Entry(root, width=50)
url_entry.pack(pady=5)

download_btn = tk.Button(root, text="Download", font=("Arial", 12), command=download_video)
download_btn.pack(pady=20)

root.mainloop()
