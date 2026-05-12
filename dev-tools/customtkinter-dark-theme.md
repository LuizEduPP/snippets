---
tags: ["python", "dev-tools", "gui", "dark-mode"]
---
# CustomTkinter Dark Theme System

Applies dark mode along with a custom dynamic JSON color theme to Python desktop applications built with the `customtkinter` engine.

## 🛠️ How it works under the hood

1. **`set_appearance_mode`**: Forces `customtkinter` to override OS variables and render the GUI exclusively in "Dark", "Light", or "System" constraints globally.
2. **Double Color Arrays**: The `.json` theme file maps styling elements using arrays composed of two elements. Index 0 is parsed for Light mode, and Index 1 corresponds to Dark mode. This means `["gray92", "gray14"]` shifts the exact same component automatically from almost white to dark gray.

---

## ⚡ Setup / Installation

Install the library:
```bash
pip install customtkinter
```

---

## 🚀 Usage Guide

### Defining a Custom JSON Theme

Save a dictionary file into your project folder. Let's call it `my_theme.json`:

```json
{
 "CTk": {
 "fg_color": ["gray92", "gray14"]
 },
 "CTkButton": {
 "fg_color": ["#3B8ED0", "#1F6AA5"],
 "hover_color": ["#36719F", "#144870"],
 "text_color": ["#DCE4EE", "#DCE4EE"]
 },
 "CTkFrame": {
 "fg_color": ["gray86", "gray17"],
 "border_color": ["gray65", "gray28"]
 }
}
```

### Implementing Python Layout

```python
import customtkinter as ctk

# Step 1. Force the appearance layout parameters
ctk.set_appearance_mode("Dark")

# Step 2. Link built-in or custom layout configurations before instantiating objects
ctk.set_default_color_theme("my_theme.json") 
# "blue", "green", and "dark-blue" are available if you don't declare a JSON.

root = ctk.CTk()
root.title("Modern Dark App")
root.geometry("800x600")

# Everything generated after the config setup will follow the exact guidelines
frame = ctk.CTkFrame(root)
frame.pack(pady=20, padx=20, fill="both", expand=True)

ctk.CTkLabel(frame, text="Night Mode Successfully Active!").pack(pady=10)
ctk.CTkButton(frame, text="Authenticate").pack(pady=10)

root.mainloop()
```
