import tkinter as tk

# Function to update input field when button is clicked
def button_click(number):
    current = entry.get()
    entry.delete(0, tk.END)
    entry.insert(0, current + str(number))

# Function to clear input
def button_clear():
    entry.delete(0, tk.END)

# Function to evaluate the expression
def button_equal():
    try:
        result = eval(entry.get())
        entry.delete(0, tk.END)
        entry.insert(0, str(result))
    except:
        entry.delete(0, tk.END)
        entry.insert(0, "Error")

# ---------------- GUI Setup ---------------- #
root = tk.Tk()
root.title("Calculator")

# Entry field
entry = tk.Entry(root, width=20, borderwidth=10, font=("Arial", 18), justify="right")
entry.grid(row=0, column=0, columnspan=4, pady=10)

# Number buttons
buttons = [
    ('7',1,0), ('8',1,1), ('9',1,2),
    ('4',2,0), ('5',2,1), ('6',2,2),
    ('1',3,0), ('2',3,1), ('3',3,2),
    ('0',4,1)
]

for (text,row,col) in buttons:
    button = tk.Button(root, text=text, padx=20, pady=20, font=("Arial", 24),
                       command=lambda t=text: button_click(t))
    button.grid(row=row, column=col)

# Operator buttons
operators = [
    ('+',1,3), ('-',2,3), ('*',3,3), ('/',4,3)
]

for (op,row,col) in operators:
    button = tk.Button(root, text=op, padx=20, pady=20, font=("Arial", 24),
                       command=lambda t=op: button_click(t))
    button.grid(row=row, column=col)

# Clear button
clear_button = tk.Button(root, text="C", padx=20, pady=20, font=("arial", 24), command=button_clear)
clear_button.grid(row=4, column=0)

# Equal button
equal_button = tk.Button(root, text="=", padx=20, pady=20, font=("arial", 24), command=button_equal)
equal_button.grid(row=4, column=2)

root.mainloop()
