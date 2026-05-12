---
tags: ["python", "tools", "qr-code", "wifi"]
---
# Generate Wi-Fi QR Code

Generates a QR code PNG that phones can scan to automatically connect to a Wi-Fi network. Supports WPA/WPA2, WEP, and open networks, with optional hidden SSID flag.

## Dependencies

```bash
pip install qrcode pillow
```

## Usage

Edit the `ssid`, `password`, and `security` values in the `__main__` block, then run the script. Each call saves a `.png` file in the current directory.

## Code

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
    Generate a QR code for Wi-Fi auto-connection.

    Args:
        ssid:     Network name (SSID)
        password: Network password (leave empty for open networks)
        security: Security type — WPA, WEP, or "" for open
        hidden:   Set True if the SSID is hidden
        filename: Output image filename
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
    # WPA2 network
    generate_wifi_qr(
        ssid="MyNetwork",
        password="my_secure_password",
        security="WPA",
        filename="wifi_home.png"
    )

    # Open network (no password)
    generate_wifi_qr(
        ssid="GuestNetwork",
        password="",
        security="",
        filename="wifi_guest.png"
    )

    # Hidden network
    generate_wifi_qr(
        ssid="HiddenNet",
        password="secret_pass",
        security="WPA",
        hidden=True,
        filename="wifi_hidden.png"
    )
```

## Wi-Fi QR format reference

```
WIFI:S:<SSID>;T:<SECURITY>;P:<PASSWORD>;H:<HIDDEN>;;
```

| Field | Values |
|-------|--------|
| `T` | `WPA` (WPA/WPA2/WPA3), `WEP`, `""` (open) |
| `H` | `true` if SSID is hidden, omit otherwise |
