---
tags: ["python", "network", "qr-code", "wifi"]
---
# Generate Wi-Fi QR Code

Builds a QR code image that mobile phones can scan to join a Wi-Fi network without typing the password.

## 🛠️ How it works under the hood

1. **Wi-Fi QR string format**: The payload is a plain text string following the `WIFI:` URI scheme — e.g., `WIFI:S:MyNet;T:WPA;P:pass123;;`. Android and iOS cameras recognize this format and trigger a network join prompt automatically when scanned.
2. **`qrcode` module**: Converts the string into a grid of black and white squares using Reed-Solomon error correction (level H), meaning the QR can still be decoded even if up to 30% of the image is obscured.
3. **`pillow`**: Renders the grid into a PNG image file at the configured size (`box_size` controls pixel size per cell, `border` sets the quiet zone around the code).

---

## 🚀 Usage Guide

### 1. Install dependencies
```bash
pip install qrcode pillow
```

### 2. Run the script
```python
import qrcode

def generate_wifi_qr(
    ssid: str,
    password: str,
    security: str = "WPA",
    hidden: bool = False,
    filename: str = "wifi_qr.png"
):
    """
    Args:
        ssid:     Network name (SSID)
        password: Network password. Leave empty for open networks.
        security: "WPA" (WPA/WPA2/WPA3), "WEP", or "" for open networks
        hidden:   True if the router does not broadcast the SSID
        filename: Output PNG filename
    """
    wifi_data = f"WIFI:S:{ssid};T:{security};P:{password};"
    if hidden:
        wifi_data += "H:true;"
    wifi_data += ";"

    qr = qrcode.QRCode(
        version=1,
        error_correction=qrcode.constants.ERROR_CORRECT_H,
        box_size=10,
        border=4,
    )
    qr.add_data(wifi_data)
    qr.make(fit=True)

    img = qr.make_image(fill_color="black", back_color="white")
    img.save(filename)
    print(f"QR code saved: {filename}")

if __name__ == "__main__":
    # WPA2 home network
    generate_wifi_qr(ssid="MyNetwork", password="my_password", security="WPA", filename="wifi_home.png")

    # Open network (no password)
    generate_wifi_qr(ssid="GuestNetwork", password="", security="", filename="wifi_guest.png")

    # Hidden SSID
    generate_wifi_qr(ssid="HiddenNet", password="secret", security="WPA", hidden=True, filename="wifi_hidden.png")
```

### Wi-Fi QR string format reference

```text
WIFI:S:<SSID>;T:<SECURITY>;P:<PASSWORD>;H:<HIDDEN>;;
```

| Field | Values |
|-------|--------|
| `T`   | `WPA` (covers WPA/WPA2/WPA3), `WEP`, or empty string for open networks |
| `H`   | `true` if the router hides the SSID broadcast; omit otherwise |
