import tkinter as tk

class Calculator(tk.Tk):
    def __init__(self):
        super().__init__()
        self.title("Calculator")
        self.geometry("400x500")
        self.resizable(0, 0)

        self.result_var = tk.StringVar()

        self.create_widgets()

    def create_widgets(self):
        entry = tk.Entry(self, textvariable=self.result_var, font=("Arial", 24), bd=10, insertwidth=2, width=14, borderwidth=4)
        entry.grid(row=0, column=0, columnspan=4)

        
        buttons = [
            '7', '8', '9', '/',
            '4', '5', '6', '*',
            '1', '2', '3', '-',
            '0', '.', '=', '+',
            'C'
        ]

        row_val = 1
        col_val = 0

        for button in buttons:
            action = lambda x=button: self.click_event(x)
            tk.Button(self, text=button, padx=20, pady=20, bd=8, font=("Arial", 18),
                      command=action).grid(row=row_val, column=col_val)

            col_val += 1
            if col_val > 3:
                col_val = 0
                row_val += 1

    def click_event(self, key):
        current_text = self.result_var.get()
        if key == 'C':
            self.result_var.set("")
        elif key == '=':
            try:
                result = str(eval(current_text))
                self.result_var.set(result)
            except:
                self.result_var.set("ERROR")
        elif key in ('+', '-', '*', '/', '.'):
            if current_text and current_text[-1] not in ('+', '-', '*', '/', '.'):
                self.result_var.set(current_text + key)
        else:
            self.result_var.set(current_text + key)

if __name__ == "__main__":
    calculator = Calculator()
    calculator.mainloop()
