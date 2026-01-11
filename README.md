<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Pro QR Code Generator</title>

<script src="https://cdn.jsdelivr.net/npm/qr-code-styling@1.6.0/lib/qr-code-styling.js"></script>

<style>
body {
    background: linear-gradient(135deg,#141e30,#243b55);
    font-family: Arial;
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
}
.container {
    background: white;
    padding: 25px;
    width: 380px;
    border-radius: 16px;
    text-align: center;
    box-shadow: 0 15px 40px rgba(0,0,0,0.3);
}
input, select, button {
    width: 100%;
    padding: 10px;
    margin: 6px 0;
    border-radius: 8px;
    border: 1px solid #ccc;
}
button {
    background: #141e30;
    color: white;
    border: none;
    cursor: pointer;
}
button:hover {
    background: #243b55;
}
#qrBox {
    margin-top: 15px;
}
</style>
</head>

<body>

<div class="container">
    <h2>Pro QR Generator</h2>

    <input type="text" id="text" placeholder="Enter text or URL">

    <label>Dot Style</label>
    <select id="dotStyle">
        <option value="rounded">Rounded</option>
        <option value="dots">Dots</option>
        <option value="classy">Classy</option>
        <option value="square">Square</option>
    </select>

    <label>QR Color</label>
    <input type="color" id="qrColor" value="#000000">

    <label>Logo Size</label>
    <input type="range" id="logoSize" min="0.1" max="0.5" step="0.05" value="0.3">

    <label>Upload Logo</label>
    <input type="file" id="logo" accept="image/*">

    <button onclick="generate()">Generate QR</button>
    <button onclick="download()">Download QR</button>

    <div id="qrBox"></div>
</div>

<script>
let qrCode;

function generate() {
    let text = document.getElementById("text").value;
    if (text === "") {
        alert("Enter text!");
        return;
    }

    let file = document.getElementById("logo").files[0];
    let logoURL = file ? URL.createObjectURL(file) : "";

    document.getElementById("qrBox").innerHTML = "";

    qrCode = new QRCodeStyling({
        width: 260,
        height: 260,
        data: text,
        image: logoURL,
        dotsOptions: {
            type: dotStyle.value,
            color: qrColor.value
        },
        imageOptions: {
            crossOrigin: "anonymous",
            imageSize: logoSize.value
        },
        backgroundOptions: {
            color: "#ffffff"
        }
    });

    qrCode.append(document.getElementById("qrBox"));
}

function download() {
    if (!qrCode) {
        alert("Generate QR first!");
        return;
    }
    qrCode.download({ name: "qr-code", extension: "png" });
}
</script>

</body>
</html>
