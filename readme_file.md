# PDF Content Extraction Tool
## AI/Python Internship Assignment - Part 1

A comprehensive Python tool for extracting content from PDF files, specifically designed for educational materials like Math Olympiad papers. This project extracts text, images, and automatically identifies questions with their corresponding visual elements.

---

## 🎯 **Project Overview**

This tool is designed to process PDF documents containing educational content and extract:
- **Text content** (page by page)
- **Images** (saved as separate PNG files)
- **Questions** (automatically identified and parsed)
- **Multiple choice options** (both text and images)
- **Structured JSON output** for further AI/ML processing

Perfect for analyzing educational materials, test papers, and question banks.

---

## 📋 **Features**

### ✅ **Core Functionality**
- **Smart PDF Processing**: Handles complex PDFs with mixed content
- **Text Extraction**: Page-by-page text extraction with UTF-8 support
- **Image Extraction**: Automatically extracts and saves all images
- **Question Recognition**: Uses pattern matching to identify various question formats
- **Option Parsing**: Recognizes multiple choice options (A, B, C, D format)
- **Structured Output**: Generates clean JSON for downstream processing

### ✅ **Advanced Features**
- **Google Colab Ready**: Optimized for cloud-based processing
- **Progress Tracking**: Real-time extraction progress updates
- **Visual Preview**: Display extracted images inline (Colab version)
- **Auto-Download**: Packages results for easy download
- **Error Handling**: Comprehensive error handling and user feedback
- **Flexible Input**: Works with various PDF formats and structures

---

## 📁 **Project Structure**

```
pdf-content-extractor/
│
├── README.md                          # This file
├── pdf_extractor.py                   # Standalone Python script
├── PDF_Content_Extractor.ipynb        # Google Colab notebook
├── requirements.txt                   # Python dependencies
│
└── sample_output/                     # Example output structure
    ├── extracted_content.json         # Main structured output
    └── images/                        # Extracted images folder
        ├── page1_image1.png
        ├── page1_image2.png
        └── ...
```

---

## 🚀 **Quick Start**

### **Option 1: Google Colab (Recommended)**

1. **Open the notebook**: Upload `PDF_Content_Extractor.ipynb` to Google Colab
2. **Run all cells**: Execute the setup and main code cells
3. **Start extraction**: Run `extracted_data = run_pdf_extraction()`
4. **Upload your PDF**: Use the file upload interface
5. **Download results**: Get the auto-generated zip package

### **Option 2: Local Python Environment**

1. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

2. **Run the script**:
   ```bash
   python pdf_extractor.py
   ```

3. **Update file path** in script if needed:
   ```python
   pdf_file_path = "your_pdf_file.pdf"
   ```

---

## 📦 **Installation**

### **Dependencies**

```bash
# Core PDF processing
pip install PyMuPDF

# Image processing
pip install Pillow

# Additional PDF capabilities
pip install pdfplumber
```

### **Quick Install**
```bash
pip install -r requirements.txt
```

### **System Requirements**
- Python 3.7+
- 2GB+ RAM (for large PDFs)
- Write permissions in working directory

---

## 🔧 **Usage Examples**

### **Basic Usage**
```python
from pdf_extractor import PDFContentExtractor

# Initialize extractor
extractor = PDFContentExtractor("sample.pdf")

# Extract content
data = extractor.extract_content()

# Access results
print(f"Found {data['total_questions']} questions")
print(f"Extracted {len(data['pages_content'])} pages")
```

### **Custom Configuration**
```python
# Custom output directory
extractor = PDFContentExtractor(
    pdf_path="input.pdf", 
    output_dir="my_custom_output"
)

# Process with custom settings
extracted_data = extractor.extract_content()
```

### **Google Colab Usage**
```python
# Simple one-liner in Colab
extracted_data = run_pdf_extraction()
```

---

## 📊 **Output Format**

### **JSON Structure**
```json
{
  "source_file": "path/to/input.pdf",
  "total_pages": 10,
  "total_questions": 25,
  "extraction_summary": {
    "pages_processed": 10,
    "total_images": 45,
    "questions_found": 25
  },
  "pages_content": [
    {
      "page_number": 1,
      "text": "Page text content...",
      "images": ["path/to/page1_image1.png"]
    }
  ],
  "questions": [
    {
      "question_number": "1",
      "question": "What is the next figure in the sequence?",
      "page": 1,
      "images": "path/to/question_image.png",
      "option_images": ["path/to/optionA.png", "path/to/optionB.png"],
      "options_text": ["A) Triangle", "B) Square"],
      "all_page_images": ["path/to/all_images_on_page.png"]
    }
  ]
}
```

### **File Organization**
```
extracted_content/
├── extracted_content.json     # Main structured data
└── images/                   # All extracted images
    ├── page1_image1.png     # Question images
    ├── page1_image2.png     # Option images
    ├── page2_image1.png     # Diagrams
    └── ...                  # Additional images
```

---

## 🎨 **Question Recognition Patterns**

The tool automatically identifies questions using these patterns:

### **Supported Question Formats**
- ❓ **Direct questions**: "What is the next figure?"
- 🔢 **Numbered questions**: "1. Find the missing number"
- 🔍 **Pattern questions**: "Complete the pattern"
- 📊 **Count questions**: "How many triangles are there?"
- 🎯 **Choice questions**: "Which option comes next?"

### **Option Recognition**
- ✅ **Standard format**: A) Option text
- ✅ **Parenthesis format**: (A) Option text
- ✅ **Mixed format**: Text + Image options

---

## 🛠️ **Customization**

### **Adding New Question Patterns**
```python
# In parse_questions_and_options method
question_patterns = [
    r'^(\d+\.?\s*)?(.+\?)\s*$',     # Questions ending with ?
    r'.*your_custom_pattern.*',      # Add your pattern here
    # ... existing patterns
]
```

### **Modifying Image Extraction**
```python
# Custom image formats and processing
def extract_images_from_pdf(self, pages_content):
    # Add custom image processing logic
    # Modify image formats, resolution, etc.
    pass
```

### **Custom Output Structure**
```python
# Modify the output_data structure in extract_content method
output_data = {
    "custom_field": "your_value",
    # ... existing structure
}
```

---

## 🔍 **Troubleshooting**

### **Common Issues**

#### **1. Module Import Errors**
```bash
# Solution
pip install --upgrade pip
pip install PyMuPDF Pillow pdfplumber
```

#### **2. PDF Not Found**
```python
# Check file path
import os
print(os.path.exists("your_file.pdf"))  # Should return True
```

#### **3. Permission Errors**
```bash
# On Linux/Mac
chmod 755 ./
# On Windows: Run as administrator
```

#### **4. Memory Issues with Large PDFs**
```python
# Process pages in batches for large files
# Monitor memory usage with smaller test files first
```

### **Debug Mode**
```python
# Enable detailed logging
import logging
logging.basicConfig(level=logging.DEBUG)
```

---

## 📈 **Performance Tips**

### **Optimization Strategies**
- ✅ **Use SSD storage** for faster I/O operations
- ✅ **Process smaller PDFs first** to test setup
- ✅ **Close other applications** when processing large files
- ✅ **Use Google Colab** for heavy processing (free GPU/RAM)

### **Expected Processing Times**
- **Small PDFs (1-5 pages)**: 10-30 seconds
- **Medium PDFs (5-20 pages)**: 1-3 minutes
- **Large PDFs (20+ pages)**: 3-10 minutes

---

## 🎯 **Next Steps (Parts 2 & 3)**

This tool provides the foundation for:

### **Part 2: AI Analysis**
- Use extracted images for computer vision tasks
- Apply OCR for enhanced text recognition
- Implement image classification for question types

### **Part 3: Question Generation**
- Leverage the structured JSON for ML model training
- Generate similar questions based on patterns
- Create automated question banks

---

## 🤝 **Contributing**

### **How to Contribute**
1. Fork the repository
2. Create a feature branch: `git checkout -b feature-name`
3. Make your changes and test thoroughly
4. Submit a pull request with detailed description

### **Areas for Improvement**
- Enhanced question pattern recognition
- Support for more PDF formats
- Advanced image processing capabilities
- Performance optimizations
- Additional output formats

---

## 📄 **License**

This project is created for educational purposes as part of an AI/Python internship assignment. Feel free to use and modify for learning and development purposes.

---

## 📞 **Support**

For issues, questions, or suggestions:

1. **Check the troubleshooting section** above
2. **Review the code comments** for implementation details
3. **Test with sample PDFs** to isolate issues
4. **Verify all dependencies** are properly installed

---

## 🏆 **Assignment Completion Status**

### ✅ **Part 1: PDF Content Extraction** - **COMPLETED**
- [x] Text extraction from PDF
- [x] Image extraction and saving
- [x] Structured JSON output
- [x] Question and option recognition
- [x] Google Colab compatibility
- [x] Comprehensive documentation

### 🔄 **Ready for Parts 2 & 3**
The structured output from this tool provides the perfect foundation for AI-based analysis and question generation in the subsequent parts of the assignment.

---

## 📊 **Technical Specifications**

| Feature | Implementation | Status |
|---------|---------------|--------|
| PDF Processing | PyMuPDF (fitz) | ✅ Complete |
| Image Extraction | PNG format, full resolution | ✅ Complete |
| Text Processing | UTF-8, page-by-page | ✅ Complete |
| Question Recognition | Regex patterns, smart parsing | ✅ Complete |
| Output Format | JSON, structured data | ✅ Complete |
| Google Colab | Full compatibility, auto-download | ✅ Complete |
| Error Handling | Comprehensive, user-friendly | ✅ Complete |
| Documentation | Complete README, code comments | ✅ Complete |

---

*Built with ❤️ for AI/Python Internship Assignment*
