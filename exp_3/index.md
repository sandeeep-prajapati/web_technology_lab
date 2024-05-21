To create a webpage that displays browser information using JavaScript, you'll need to capture details such as the browser name, version, platform, and other relevant information. Here’s a step-by-step guide to achieve this:

### Step 1: Create the HTML File (browser_info.html)
This HTML file will contain the structure of your webpage and a script to gather and display the browser information.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Browser Information</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 20px;
        }
        .container {
            max-width: 600px;
            margin: auto;
            background: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        h1 {
            text-align: center;
            color: #333;
        }
        p {
            font-size: 1.1em;
            margin-bottom: 10px;
        }
        .info-item {
            margin: 10px 0;
        }
        .info-item span {
            font-weight: bold;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Browser Information</h1>
        <div class="info-item"><span>Browser Name:</span> <span id="browserName"></span></div>
        <div class="info-item"><span>Browser Version:</span> <span id="browserVersion"></span></div>
        <div class="info-item"><span>Platform:</span> <span id="platform"></span></div>
        <div class="info-item"><span>User Agent:</span> <span id="userAgent"></span></div>
        <div class="info-item"><span>Cookies Enabled:</span> <span id="cookiesEnabled"></span></div>
        <div class="info-item"><span>Language:</span> <span id="language"></span></div>
        <div class="info-item"><span>Online Status:</span> <span id="onlineStatus"></span></div>
    </div>
    <script>
        // Function to get browser information
        function getBrowserInfo() {
            const userAgent = navigator.userAgent;
            const platform = navigator.platform;
            const language = navigator.language;
            const online = navigator.onLine;
            const cookiesEnabled = navigator.cookieEnabled;

            // Browser name and version extraction
            let browserName = "Unknown Browser";
            let browserVersion = "Unknown Version";
            if (/chrome|crios|crmo/i.test(userAgent)) {
                browserName = "Chrome";
                browserVersion = userAgent.match(/(?:chrome|crios|crmo)\/(\d+)/i)[1];
            } else if (/firefox|iceweasel|fxios/i.test(userAgent)) {
                browserName = "Firefox";
                browserVersion = userAgent.match(/(?:firefox|iceweasel|fxios)\/(\d+)/i)[1];
            } else if (/safari/i.test(userAgent) && !/chrome|crios|crmo/i.test(userAgent)) {
                browserName = "Safari";
                browserVersion = userAgent.match(/version\/(\d+)/i)[1];
            } else if (/msie|trident/i.test(userAgent)) {
                browserName = "Internet Explorer";
                browserVersion = userAgent.match(/(?:msie |rv:)(\d+)/i)[1];
            } else if (/edg/i.test(userAgent)) {
                browserName = "Edge";
                browserVersion = userAgent.match(/edg\/(\d+)/i)[1];
            } else if (/opera|opr|opios/i.test(userAgent)) {
                browserName = "Opera";
                browserVersion = userAgent.match(/(?:opera|opr|opios)[\s\/](\d+)/i)[1];
            }

            // Display the information in the HTML
            document.getElementById("browserName").textContent = browserName;
            document.getElementById("browserVersion").textContent = browserVersion;
            document.getElementById("platform").textContent = platform;
            document.getElementById("userAgent").textContent = userAgent;
            document.getElementById("cookiesEnabled").textContent = cookiesEnabled ? "Yes" : "No";
            document.getElementById("language").textContent = language;
            document.getElementById("onlineStatus").textContent = online ? "Online" : "Offline";
        }

        // Call the function to get browser information on page load
        window.onload = getBrowserInfo;
    </script>
</body>
</html>
```

### Explanation
1. **HTML Structure**:
    - The HTML file includes a basic structure with a container to display the browser information.
    - Each piece of information (e.g., browser name, version) is displayed in its own `div` with the class `info-item`.

2. **CSS Styling**:
    - Basic styles are applied for readability and visual appeal.
    - The container is centered, and a shadow effect is added for better presentation.

3. **JavaScript**:
    - The `getBrowserInfo` function gathers various pieces of browser information using the `navigator` object.
    - It extracts the browser name and version using regular expressions on the `userAgent` string.
    - It then updates the HTML elements with the corresponding IDs to display the gathered information.

### Running the Web Page
1. Save the file as `browser_info.html`.
2. Open the file in a web browser to see the browser information displayed.

This setup provides a simple yet effective way to display comprehensive browser information on a web page using HTML and JavaScript.