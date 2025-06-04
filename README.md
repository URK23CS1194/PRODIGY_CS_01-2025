import tkinter as tk
from tkinter import messagebox

def caesar_cipher(text, shift, mode):
    result = ""
    for char in text:
        if char.isalpha():
            base = ord('A') if char.isupper() else ord('a')
            shift_val = shift if mode == "Encrypt" else -shift
            result += chr((ord(char) - base + shift_val) % 26 + base)
        else:
            result += char
    return result
def process_text_cipher():
    text = entry_text.get("1.0", tk.END).strip()
    try:
        shift = int(entry_shift.get())
        mode = mode_var.get()
        if not text:
            messagebox.showwarning("Input Error", "Enter a message to process.")
            return
        result = caesar_cipher(text, shift, mode)
        output_text.delete("1.0", tk.END)
        output_text.insert(tk.END, result)
    except ValueError:
        messagebox.showerror("Shift Error", "Shift must be an integer.")
win = tk.Tk()
win.title("Caesar Cipher - ProDigy Infotech")
win.geometry("500x450")
win.config(bg="lightblue")
tk.Label(win, text="Caesar Cipher Encryption/Decryption", font=("Arial", 16, "bold"), bg="lightblue").pack(pady=10)
frame = tk.Frame(win, bg="lightblue")
frame.pack()
tk.Label(frame, text="Enter your message:", bg="lightblue").pack()
entry_text = tk.Text(frame, height=5, width=50)
entry_text.pack()
tk.Label(frame, text="Enter Shift Value:", bg="lightblue").pack()
entry_shift = tk.Entry(frame)
entry_shift.pack()
mode_var = tk.StringVar(value="Encrypt")
tk.Radiobutton(frame, text="Encrypt", variable=mode_var, value="Encrypt", bg="lightblue").pack()
tk.Radiobutton(frame, text="Decrypt", variable=mode_var, value="Decrypt", bg="lightblue").pack()
tk.Button(frame, text="Process", command=process_text_cipher, bg="blue", fg="white").pack(pady=5)
tk.Label(frame, text="Output:", bg="lightblue").pack()
output_text = tk.Text(frame, height=4, width=50, bg="lightyellow")
output_text.pack()
win.mainloop()
