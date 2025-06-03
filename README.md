import tkinter as tk
from tkinter import ttk

def converter():
    try:
        temp = float(temperature.get())  # get the number typed in input box
        unit = units.get()  # get the selected unit (Celsius, Fahrenheit, Kelvin)

        if unit == "Celsius":
            fahrenheit = (temp * 9/5) + 32
            kelvin = temp + 273.15
            result.set(f"{temp}°C = {fahrenheit:.2f}°F, {kelvin:.2f}K")

        elif unit == "Fahrenheit":
            celsius = (temp - 32) * 5/9
            kelvin = celsius + 273.15
            result.set(f"{temp}°F = {celsius:.2f}°C, {kelvin:.2f}K")

        elif unit == "Kelvin":
            celsius = temp - 273.15
            fahrenheit = (celsius * 9/5) + 32
            result.set(f"{temp}K = {celsius:.2f}°C, {fahrenheit:.2f}°F")

        else:
            result.set("Please select a valid unit.")

    except ValueError:
        result.set("Please enter a valid number.")

# GUI design
window = tk.Tk()
window.title("Temperature Converter")
window.geometry("400x300")
window.resizable(False, False)

# Label and Entry for temperature input
tk.Label(window, text="Enter Temperature:", font=("Arial", 12)).pack(pady=5)
temperature = tk.Entry(window, font=("Arial", 12))
temperature.pack(pady=5)

# Unit selection dropdown
tk.Label(window, text="Select Unit:", font=("Arial", 12)).pack(pady=5)
units = tk.StringVar()
units.set("Celsius")  # default value
unit_menu = ttk.Combobox(window, textvariable=units,
                         values=["Celsius", "Fahrenheit", "Kelvin"],
                         state="readonly", font=("Arial", 12))
unit_menu.pack(pady=5)

# Convert button
convert_btn = tk.Button(window, text="Convert", command=converter,
                        font=("Arial", 12), bg="lightblue")
convert_btn.pack(pady=10)

# Label to show result
result = tk.StringVar()
tk.Label(window, textvariable=result, font=("Arial", 12), fg="green",
         wraplength=350, justify="center").pack(pady=10)

# Run the app
window.mainloop()
