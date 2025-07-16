# Tech for Girls - Registration Website

A beautiful, modern registration website for the Tech for Girls community with advanced features including WhatsApp sharing, file uploads, and Google Sheets integration.

## Features

✅ **Beautiful UI Design**
- Modern gradient backgrounds and smooth animations
- Responsive design that works on all devices
- Clean, professional interface with hover effects
- Step-by-step form progression

✅ **Complete Registration Form**
- Name, phone, email, and college/department fields
- Real-time form validation
- Error handling and user feedback

✅ **WhatsApp Sharing System**
- Interactive share button with click counter
- Requires 5 shares before form submission
- Progress bar and completion indicators
- Pre-written sharing message

✅ **File Upload System**
- Drag and drop file upload
- File size validation (5MB limit)
- Visual feedback and file preview
- Support for image files

✅ **Single Submission Protection**
- localStorage-based submission tracking
- Form disabling after submission
- Success page with confirmation message

✅ **Google Sheets Integration Ready**
- Structured data format for Google Apps Script
- Base64 file encoding for image uploads
- Timestamp tracking

## Setup Instructions

### 1. Clone and Install
```bash
git clone <your-repo-url>
cd tech-for-girls-registration
npm install
```

### 2. Development
```bash
npm run dev
```

### 3. Build for Production
```bash
npm run build
```

### 4. Google Sheets Integration

To connect this form to Google Sheets:

1. **Create a Google Apps Script:**
   - Go to [script.google.com](https://script.google.com)
   - Create a new project
   - Replace the default code with:

```javascript
function doPost(e) {
  try {
    const data = JSON.parse(e.postData.contents);
    
    // Open your Google Sheet
    const sheet = SpreadsheetApp.openById('YOUR_SHEET_ID').getActiveSheet();
    
    // Add headers if this is the first row
    if (sheet.getLastRow() === 0) {
      sheet.appendRow(['Name', 'Phone', 'Email', 'College', 'Screenshot', 'Timestamp']);
    }
    
    // Add the data
    sheet.appendRow([
      data.name,
      data.phone,
      data.email,
      data.college,
      data.screenshot ? 'Screenshot uploaded' : 'No screenshot',
      data.timestamp
    ]);
    
    return ContentService
      .createTextOutput(JSON.stringify({ success: true }))
      .setMimeType(ContentService.MimeType.JSON);
      
  } catch (error) {
    return ContentService
      .createTextOutput(JSON.stringify({ error: error.toString() }))
      .setMimeType(ContentService.MimeType.JSON);
  }
}
```

2. **Deploy as Web App:**
   - Click "Deploy" > "New deployment"
   - Choose "Web app" as type
   - Set execute as "Me" and access to "Anyone"
   - Copy the deployment URL

3. **Update the Code:**
   - Replace `YOUR_GOOGLE_APPS_SCRIPT_URL_HERE` in `src/App.tsx` with your deployment URL
   - Uncomment the fetch request in the handleSubmit function

### 5. Deploy to GitHub Pages

1. **Push to GitHub:**
```bash
git add .
git commit -m "Initial commit"
git push origin main
```

2. **Enable GitHub Pages:**
   - Go to repository Settings > Pages
   - Select "GitHub Actions" as source
   - The site will be automatically deployed

## Project Structure

```
src/
├── App.tsx          # Main registration form component
├── main.tsx         # React entry point
├── index.css        # Tailwind CSS imports
└── vite-env.d.ts    # TypeScript definitions
```

## Technologies Used

- **React 18** with TypeScript
- **Tailwind CSS** for styling
- **Lucide React** for icons
- **Vite** for build tooling
- **Google Apps Script** for backend integration

## Form Validation

The form includes comprehensive validation:
- Required field validation
- Email format validation
- Phone number format validation (10 digits)
- File size validation (5MB limit)
- Share completion validation

## Features Highlight

### WhatsApp Sharing
- Custom message: "Hey Buddy, Join Tech For Girls Community! 🚀👩‍💻"
- Visual progress tracking
- Prevents form submission until 5 shares completed

### File Upload
- Supports drag and drop
- Real-time file size validation
- Visual feedback for upload status
- Secure base64 encoding for transmission

### Single Submission
- Uses localStorage to track submission status
- Prevents duplicate submissions
- Shows success page after submission

## License

This project is created for educational purposes as part of the Tech for Girls initiative.