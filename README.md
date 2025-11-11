# Envelope Merge Print

A Google Apps Script tool for automating the mail merge printing process from Google Sheets to PDF files. This script generates multiple PDF files from a spreadsheet, perfect for creating envelopes or labels with personalized information.

## Features

- **Automated PDF Generation**: Exports a Google Sheets worksheet as PDF files
- **Batch Processing**: Generates multiple PDFs in a single run (default: 14 files)
- **Google Drive Integration**: Automatically saves generated PDFs to a designated folder
- **Customizable PDF Settings**: Pre-configured with A4 landscape orientation and optimal margins
- **Japanese Language Support**: Designed for mail merge workflows (差込印刷)

## Prerequisites

- A Google Account with access to Google Sheets and Google Drive
- Basic familiarity with Google Apps Script
- A Google Sheets spreadsheet with:
  - A worksheet named "差込印刷" (mail merge)
  - A "PDF" folder in the same Google Drive location as the spreadsheet

## Setup Instructions

1. **Create Your Spreadsheet**:
   - Create a new Google Sheets spreadsheet or open an existing one
   - Create a worksheet named "差込印刷"
   - Set up your mail merge template in this worksheet

2. **Create PDF Output Folder**:
   - In Google Drive, navigate to the same folder containing your spreadsheet
   - Create a subfolder named "PDF" where the generated PDFs will be saved

3. **Add the Script**:
   - Open your Google Sheets spreadsheet
   - Go to **Extensions** → **Apps Script**
   - Delete any default code in the script editor
   - Copy the contents of `Code.js` from this repository
   - Paste it into the script editor
   - Save the project (give it a name like "Envelope Merge Print")

4. **Authorize the Script**:
   - The first time you run the script, Google will ask for permissions
   - Review and authorize the required permissions:
     - Access to Google Sheets
     - Access to Google Drive
     - Ability to make external requests

## Usage

1. **Prepare Your Data**:
   - Ensure your "差込印刷" worksheet contains the data you want to merge
   - The script uses cell A1 to iterate through different group numbers (1-14)

2. **Run the Script**:
   - In the Apps Script editor, select the `exportPDF` function
   - Click the **Run** button (▶️)
   - The script will generate 14 PDF files, numbered 1 through 14
   - Each PDF will be saved to the "PDF" folder in Google Drive

3. **Monitor Progress**:
   - Check the execution log in Apps Script for progress messages
   - The script pauses 6 seconds between each PDF generation to avoid rate limits

## Configuration

You can customize the script behavior by modifying these parameters in `Code.js`:

### Number of PDFs
Change the array length to generate more or fewer PDFs:
```javascript
for (let groupNum of ([...Array(14)].map((_, i) => i + 1))) {
    // Change 14 to your desired number
}
```

### PDF Settings
Modify the `pdfOptions` string to customize the output:
- **size**: Paper size (default: A4)
- **portrait**: Orientation (default: false for landscape)
- **fitw**: Fit to width (default: true)
- **margins**: top_margin, bottom_margin, left_margin, right_margin (default: 0.1)
- **alignment**: horizontal_alignment, vertical_alignment

### Delay Between PDFs
Adjust the sleep time (in milliseconds):
```javascript
Utilities.sleep(6000); // 6 seconds, adjust as needed
```

## How It Works

1. The script accesses the active Google Sheets spreadsheet
2. It locates the "差込印刷" worksheet
3. For each iteration (1-14):
   - Updates cell A1 with the current group number
   - Exports the worksheet as a PDF with the specified settings
   - Saves the PDF to the "PDF" folder with the group number as filename
   - Waits 6 seconds before the next iteration

## Troubleshooting

**Error: "Cannot find sheet named '差込印刷'"**
- Ensure you have created a worksheet with exactly this name

**Error: "Cannot find folder named 'PDF'"**
- Create a "PDF" folder in the same Google Drive location as your spreadsheet

**PDFs not generating**
- Check the execution log for error messages
- Verify you have authorized all required permissions
- Ensure your spreadsheet is saved in Google Drive

**Rate limit errors**
- Increase the `Utilities.sleep()` delay between PDF generations

## License

This project is provided as-is for use in mail merge and envelope printing workflows.

## Contributing

Feel free to fork this repository and customize it for your specific needs.