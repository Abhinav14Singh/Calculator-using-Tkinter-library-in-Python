import tkinter as tk

def button_click(char):
    current_text = entry.get()
    entry.delete(0, tk.END)
    entry.insert(tk.END, current_text + char)

def evaluate():
    try:
        expression = entry.get().replace('×', '*').replace('÷', '/')
        result = eval(expression)
        
        if isinstance(result, float) and result.is_integer():
            result = int(result) 
        
        entry.delete(0, tk.END)
        entry.insert(tk.END, str(result))
    except Exception as e:
        entry.delete(0, tk.END)
        entry.insert(tk.END, "Error")

def clear():
    entry.delete(0, tk.END)

root = tk.Tk()
root.title("Calculator")

entry = tk.Entry(root, width=16, font=("Arial", 24), borderwidth=2, relief="solid", justify="right")
entry.grid(row=0, column=0, columnspan=4)

buttons = [
    ('7', 1, 0), ('8', 1, 1), ('9', 1, 2),
    ('4', 2, 0), ('5', 2, 1), ('6', 2, 2),
    ('1', 3, 0), ('2', 3, 1), ('3', 3, 2),
    ('0', 4, 1), ('+', 1, 3), ('-', 2, 3),
    ('×', 3, 3), ('÷', 4, 3),
    ('C', 4, 0), ('=', 4, 2)
]

for (text, row, col) in buttons:
    if text == '=':
        btn = tk.Button(root, text=text, width=5, height=2, font=("Arial", 18), command=evaluate)
    elif text == 'C':
        btn = tk.Button(root, text=text, width=5, height=2, font=("Arial", 18), command=clear)
    else:
        btn = tk.Button(root, text=text, width=5, height=2, font=("Arial", 18), command=lambda char=text: button_click(char))
    btn.grid(row=row, column=col)

root.mainloop()
