---
tags: ["python", "tools", "customtkinter", "gui", "dark-mode"]
---
# CustomTkinter Dark Theme

Applies dark mode and a color theme to a Python desktop app built with `customtkinter`. Supports built-in themes and custom JSON color schemes.

## Dependencies

```bash
pip install customtkinter
```

## Code

### Apply theme before creating the window

```python
import customtkinter as ctk

# Appearance: "Dark", "Light", or "System"
ctk.set_appearance_mode("Dark")

# Built-in color themes: "blue", "green", "dark-blue"
ctk.set_default_color_theme("blue")

root = ctk.CTk()
root.title("My App")
root.geometry("800x600")

frame = ctk.CTkFrame(root)
frame.pack(pady=20, padx=20, fill="both", expand=True)

ctk.CTkLabel(frame, text="Hello World").pack(pady=10)
ctk.CTkButton(frame, text="Click Me").pack(pady=10)

root.mainloop()
```

---

### Custom JSON color theme

Save a file `my_theme.json`:

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

Apply it:

```python
ctk.set_default_color_theme("my_theme.json")
```

---

## Notes

- Call `set_appearance_mode` and `set_default_color_theme` **before** creating any widget.
- `"System"` follows the OS dark/light mode automatically.
- CustomTkinter widgets map `[light_value, dark_value]` for every color property.
