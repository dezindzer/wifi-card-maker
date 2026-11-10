# WiFi Card Maker

A single-page tool for designing printable WiFi cards with a scannable QR code. Guests scan the code with their phone camera and join the network without typing the password.

Everything runs in the browser. Nothing is sent to a server, and the network name and password never leave your computer.

## Getting started

1. Open `index.html` in Chrome, Edge or Firefox.
2. Enter the WiFi name, password and custom text.
3. Adjust the styling. The preview on the right updates as you type.
4. Click **Download PDF** (or **Download PNG**).

An internet connection is needed when the page loads. The QR library, the PDF library and the fonts are loaded from a CDN:

- [qr-code-styling 1.6.0-rc.1](https://www.npmjs.com/package/qr-code-styling) (jsDelivr)
- [jsPDF 2.5.1](https://cdnjs.com/libraries/jspdf) (cdnjs)
- Google Fonts

## Card layout

From top to bottom:

1. Custom text (wraps over several lines; press Enter for a new line)
2. WiFi name (bold and larger by default)
3. QR code
4. WiFi symbol with a separator line on each side
5. "Password:" label (bold; the text can be changed, for example to "Lozinka:")
6. Password

All elements are centered vertically by default. You can also start them from the top or spread them evenly.

## Features

### Card size
- Default: **95 × 150 mm**.
- Presets: 100 × 150 (4 × 6″), 105 × 148 (A6), 90 × 130, 127 × 178 (5 × 7″), 99 × 210 (DL), 148 × 210 (A5).
- Custom width and height in mm, plus a **Rotate** button that swaps them.

### Network
- Security type: WPA/WPA2/WPA3, WEP, or open (no password).
- Hidden network option.
- Option to leave the password off the printed card. It stays in the QR code.

### Text styles
The custom text, WiFi name, password label and password are each styled separately:
- Font: Montserrat, Roboto, Open Sans, Poppins, Lato, Nunito, Raleway, Merriweather, Playfair Display, Arial, Georgia or Times New Roman.
- Size in pt.
- Bold, italic and underline.
- Left, center or right alignment.
- Color.

Serbian Latin characters (č, ć, š, ž, đ) are supported.

### QR code
- Size and quiet zone (blank margin) in mm.
- Error correction: L, M, Q (default) or H.
- Dots: square, dots, rounded, extra rounded, classy or classy rounded. You can set one color or a linear or radial gradient.
- Corner squares and corner dots: shape and color, set separately.
- Background color, or a transparent background.
- Optional center logo. Error correction switches to H automatically when you add one.
- One-click presets: Classic, Soft, Dots and Elegant.

### WiFi symbol and separator
- Symbol: plain arcs or arcs inside a filled circle, with size and color.
- Separator line: solid, dashed or dotted, with thickness, length (% of the width) and gap to the symbol.

### Page and border
- Page background color, inner padding, spacing between elements, and the gap between the label and the password.
- Border: solid, dashed, dotted or double, with width, color, corner radius and distance from the edge.

### Cutting guides
- **None**: the PDF is exactly the card size.
- **Thin cut line** around the card.
- **Crop marks** on the four corners, as used in print production.
- **Cut line + crop marks**.

When guides are on, the card is placed on a larger sheet: either the card plus a margin (10 mm by default) or the center of an A4 sheet. You can also set the mark length, the mark gap from the edge, the line thickness and the bleed (how far the page color extends past the cut edge).

### Export and settings
- PDF at 300 or 600 dpi (600 by default), and PNG.
- Files are named after the network, for example `wifi-Guest-WiFi.pdf`.
- **Save design** writes all settings to a `.json` file, and **Load design** restores them.
- The last design is remembered in the browser automatically.
- **Reset to defaults** restores the original design.

## Printing tips

- **Print at 100% / "Actual size".** Turn off "Fit to page" in the print dialog, or the card will not match the holder.
- **Measure the inside of the holder** and enter those dimensions. If the holder's frame covers the edges, increase the inner padding.
- **For a print shop:** use crop marks with 2–3 mm bleed and no cut line. A cut line can stay visible on the edge if the cut is slightly off.
- **For cutting by hand:** the thin cut line is the easiest to follow.
- **Use dark dots on a light background** for the QR code. Some phone cameras cannot read light-on-dark or low-contrast codes.
- **Keep the QR code at 40 mm or larger** so it scans easily from a distance.
- **Test a printed card with an iPhone and an Android phone** before printing a batch.

## Technical notes

- The card is drawn on an HTML canvas. The same drawing code is used for the preview and the export.
- The PDF contains a high-resolution image of the card (2244 × 3543 px for 95 × 150 mm at 600 dpi), not editable text. This is because the PDF library's built-in fonts cannot show characters like č or đ.
- The QR code uses the standard WiFi format `WIFI:T:<type>;S:<ssid>;P:<password>;H:<hidden>;;`. The special characters `\ ; , : "` are escaped.
