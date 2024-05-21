To create a well-structured XML document with a DTD (Document Type Definition) and display it using a stylesheet, you need to follow these steps:

1. **Create the XML Document**.
2. **Create the DTD File**.
3. **Create the XSL Stylesheet**.
4. **Link the XML Document with the DTD and XSL**.

Here's a step-by-step guide:

### Step 1: Create the XML Document (students.xml)
This XML file contains the data that you want to display.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE students SYSTEM "students.dtd">
<?xml-stylesheet type="text/xsl" href="students.xsl"?>
<students>
    <student>
        <name>John Doe</name>
        <email>john.doe@example.com</email>
        <phone>(123) 456-7890</phone>
        <address>1234 Elm Street, Springfield, IL</address>
        <course>BSc</course>
    </student>
    <student>
        <name>Jane Smith</name>
        <email>jane.smith@example.com</email>
        <phone>(987) 654-3210</phone>
        <address>5678 Oak Avenue, Metropolis, NY</address>
        <course>MSc</course>
    </student>
</students>
```

### Step 2: Create the DTD File (students.dtd)
This DTD file defines the structure and rules for the XML document.

```dtd
<!ELEMENT students (student+)>
<!ELEMENT student (name, email, phone, address, course)>
<!ELEMENT name (#PCDATA)>
<!ELEMENT email (#PCDATA)>
<!ELEMENT phone (#PCDATA)>
<!ELEMENT address (#PCDATA)>
<!ELEMENT course (#PCDATA)>
```

### Step 3: Create the XSL Stylesheet (students.xsl)
This XSL file transforms the XML data into HTML for display in a browser.

```xsl
<?xml version="1.0" encoding="UTF-8"?>
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
    <xsl:template match="/">
        <html>
        <head>
            <title>Student Information</title>
            <style>
                body {
                    font-family: Arial, sans-serif;
                    background-color: #f4f4f4;
                    padding: 20px;
                }
                .container {
                    max-width: 800px;
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
                table {
                    width: 100%;
                    border-collapse: collapse;
                    margin: 20px 0;
                }
                th, td {
                    padding: 10px;
                    border: 1px solid #ddd;
                    text-align: left;
                }
                th {
                    background-color: #007BFF;
                    color: white;
                }
                tr:nth-child(even) {
                    background-color: #f2f2f2;
                }
            </style>
        </head>
        <body>
            <div class="container">
                <h1>Student Information</h1>
                <table>
                    <tr>
                        <th>Name</th>
                        <th>Email</th>
                        <th>Phone</th>
                        <th>Address</th>
                        <th>Course</th>
                    </tr>
                    <xsl:for-each select="students/student">
                        <tr>
                            <td><xsl:value-of select="name"/></td>
                            <td><xsl:value-of select="email"/></td>
                            <td><xsl:value-of select="phone"/></td>
                            <td><xsl:value-of select="address"/></td>
                            <td><xsl:value-of select="course"/></td>
                        </tr>
                    </xsl:for-each>
                </table>
            </div>
        </body>
        </html>
    </xsl:template>
</xsl:stylesheet>
```

### Explanation:

1. **XML Document**:
   - The XML document (`students.xml`) includes a reference to the DTD file and the XSL stylesheet.
   - It contains sample data for students.

2. **DTD File**:
   - The DTD (`students.dtd`) defines the structure of the XML document, specifying that a `students` element contains one or more `student` elements, and each `student` contains `name`, `email`, `phone`, `address`, and `course` elements.

3. **XSL Stylesheet**:
   - The XSL file (`students.xsl`) transforms the XML data into an HTML table for display in a browser.
   - It includes inline CSS for styling the HTML output.

### Step 4: Viewing the Document
1. Ensure all three files (`students.xml`, `students.dtd`, `students.xsl`) are in the same directory.
2. Open `students.xml` in a web browser that supports XSLT, such as Internet Explorer.

### Conclusion
This example demonstrates how to create an XML document with a DTD and display it using XSLT. This approach ensures your XML data adheres to a defined structure and can be transformed into a readable format in a web browser.