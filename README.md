import tkinter as tk
from tkinter import messagebox
import numpy as np

root = tk.Tk()
root.geometry("600x600")
root.title("Temperature Converter using Tkinter")

#---main frame---
main_frame = tk.Frame(root, pady=10, width=500, bg="light blue", height=500, border=50)
main_frame.pack(pady=50)
main_frame.pack_propagate(False)

# --- label ---
userlabel = tk.Label(main_frame, text="Temperature Fahrenheit to Celsius", 
                  font=("Arial", 12, "bold"), bg="light blue", fg="black")
userlabel.pack()

# --- input frame ---
input_frame = tk.Frame(main_frame)
input_frame.pack(pady=20)

input_box = tk.Entry(input_frame, width=10)
input_box.grid(row=0, column=0)

# --- answer entry ---
answer = tk.Entry(main_frame, state="readonly", width=11)
answer.pack(pady=10)

stack = []

# --- functions ---
def change_temp():
 user = input_box.get().strip()
 if user == "":
     messagebox.showinfo("Error", "Please enter a number")
     return
 
 if user.replace(".", "", 1).isdigit():  # allows float numbers
     value = float(user)
     formula = np.round((value - 32) * 5 / 9, 2)
     
     answer.config(state="normal")
     answer.delete(0, tk.END)
     answer.insert(0, formula)
     answer.config(state="readonly")
 else:
     messagebox.showinfo("Wrong", "Enter only numbers")

def clear():
 answer_value = answer.get()
 if answer_value:
     stack.append(answer_value)
     print("Stack:", stack)

 input_value = input_box.get()
 if input_value:
     stack.append(input_value)
     print("Stack:", stack)

 answer.config(state="normal")
 answer.delete(0, tk.END)
 answer.config(state="readonly")
 input_box.delete(0, tk.END)

def undo_data():
 if len(stack) >= 2:
     d = stack[-1]   # input value
     s = stack[-2]   # answer value

     input_box.insert(0, d)
     answer.config(state="normal")
     answer.insert(0, s)
     answer.config(state="readonly")

# --- buttons ---
convert_button = tk.Button(main_frame, text="Convert", 
                        font=("Arial", 12, "bold"), width=10, 
                        bg="#34495e", fg="white", command=change_temp)
convert_button.pack(pady=30)

delete = tk.Button(main_frame, text="Clear", command=clear, 
                font=("Arial", 12, "bold"), width=10, bg="#34495e", fg="white")
delete.pack()

undo = tk.Button(main_frame, text="Undo", width=10, 
              font=("Arial", 12, "bold"), command=undo_data)
undo.pack(pady=30)

root.mainloop()
