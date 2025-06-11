# PDF Q&A Application

A full-stack application that allows users to upload PDF documents and ask questions about their content using natural language processing. The application leverages AI to provide intelligent answers based on the uploaded document content.

## 🚀 Features

- **PDF Upload**: Upload PDF documents with drag-and-drop or file selection
- **Text Extraction**: Automatic text extraction from uploaded PDFs
- **AI-Powered Q&A**: Ask questions about document content and receive intelligent answers
- **Follow-up Questions**: Ask multiple questions on the same document
- **Document Management**: View uploaded documents and their metadata
- **Real-time Processing**: Live feedback during upload and question processing
- **Error Handling**: Comprehensive error messages for unsupported files or processing issues

## 🛠️ Technology Stack

### Backend
- **FastAPI**: High-performance Python web framework
- **LangChain/LlamaIndex**: Natural language processing and document querying
- **PyMuPDF**: PDF text extraction
- **SQLite/PostgreSQL**: Document metadata storage
- **Python 3.8+**: Core backend language

### Frontend
- **React.js**: Modern JavaScript library for building user interfaces
- **JavaScript/TypeScript**: Frontend development
- **CSS3/Tailwind**: Styling and responsive design

### Additional Tools
- **Vector Stores**: For efficient document embedding storage
- **File Storage**: Local filesystem for PDF storage

## 📁 Project Structure

```
PROJECT/
├── backend/
│   ├── uploads/                    # Uploaded PDF files
│   ├── vector_stores/              # Document embeddings storage
│   │   ├── 1bb102c0-68db-48ac-b543-fb04ff6e89d1/
│   │   └── a66a3a71-df8e-444a-a3c6-80e31fcd9ea6/
│   ├── __pycache__/               # Python cache files
│   ├── main.py                    # FastAPI application entry point
│   ├── models.py                  # Database models
│   ├── pdf_processor.py           # PDF processing logic
│   ├── question_answering.py      # Q&A logic using LangChain
│   └── requirements.txt           # Python dependencies
└── src/
    ├── components/                # React components
    ├── App.js                     # Main React application
    ├── package.json               # Node.js dependencies
    └── public/                    # Static assets
```

## 🚀 Getting Started

### Prerequisites

- Python 3.8 or higher
- Node.js 14 or higher
- npm or yarn package manager

### Backend Setup

1. **Navigate to the backend directory:**
   ```bash
   cd backend
   ```

2. **Create a virtual environment:**
   ```bash
   python -m venv venv
   
   # On Windows
   venv\Scripts\activate
   
   # On macOS/Linux
   source venv/bin/activate
   ```

3. **Install Python dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Set up environment variables:**
   Create a `.env` file in the backend directory:
   ```
   DATABASE_URL=sqlite:///./app.db
   OPENAI_API_KEY=your_openai_api_key_here
   UPLOAD_DIR=./uploads
   VECTOR_STORE_DIR=./vector_stores
   ```

5. **Initialize the database:**
   ```bash
   python -c "from models import create_tables; create_tables()"
   ```

6. **Start the FastAPI server:**
   ```bash
   uvicorn main:app --reload --host 0.0.0.0 --port 8000
   ```

The backend API will be available at `http://localhost:8000`

### Frontend Setup

1. **Navigate to the src directory:**
   ```bash
   cd src
   ```

2. **Install Node.js dependencies:**
   ```bash
   npm install
   # or
   yarn install
   ```

3. **Start the React development server:**
   ```bash
   npm start
   # or
   yarn start
   ```

The frontend application will be available at `http://localhost:3000`

## 📚 API Documentation

### Endpoints

#### Upload PDF
- **POST** `/upload-pdf`
- **Description**: Upload a PDF document
- **Content-Type**: `multipart/form-data`
- **Parameters**: 
  - `file`: PDF file (required)
- **Response**: 
  ```json
  {
    "document_id": "uuid",
    "filename": "document.pdf",
    "message": "PDF uploaded successfully"
  }
  ```

#### Ask Question
- **POST** `/ask-question`
- **Description**: Ask a question about an uploaded PDF
- **Content-Type**: `application/json`
- **Body**:
  ```json
  {
    "document_id": "uuid",
    "question": "What is the main topic of this document?"
  }
  ```
- **Response**:
  ```json
  {
    "answer": "The main topic is...",
    "confidence": 0.95,
    "sources": ["page 1", "page 3"]
  }
  ```

#### Get Documents
- **GET** `/documents`
- **Description**: Retrieve list of uploaded documents
- **Response**:
  ```json
  {
    "documents": [
      {
        "id": "uuid",
        "filename": "document.pdf",
        "upload_date": "2024-01-01T00:00:00Z",
        "page_count": 10
      }
    ]
  }
  ```

### API Documentation
Visit `http://localhost:8000/docs` for interactive API documentation (Swagger UI)

## 🎨 Design Reference

The application follows the design specifications provided in the Figma file. Key design elements include:
- Clean, modern interface
- Intuitive upload area with drag-and-drop functionality
- Clear question input and answer display sections
- Responsive design for various screen sizes

## 🧪 Testing

### Backend Testing
```bash
cd backend
python -m pytest tests/ -v
```

### Frontend Testing
```bash
cd src
npm test
# or
yarn test
```

## 🔧 Configuration

### Environment Variables

#### Backend (.env)
```
DATABASE_URL=sqlite:///./app.db
OPENAI_API_KEY=your_api_key
UPLOAD_DIR=./uploads
VECTOR_STORE_DIR=./vector_stores
MAX_FILE_SIZE=10485760  # 10MB
ALLOWED_EXTENSIONS=pdf
```

#### Frontend (.env)
```
REACT_APP_API_URL=http://localhost:8000
REACT_APP_MAX_FILE_SIZE=10485760
```

## 📈 Performance Optimization

- **Chunking**: Large PDFs are processed in chunks for better performance
- **Caching**: Vector embeddings are cached for faster subsequent queries
- **Async Processing**: Non-blocking PDF processing using FastAPI's async capabilities
- **File Size Limits**: Configurable file size limits to prevent server overload

## 🚨 Error Handling

The application handles various error scenarios:
- Unsupported file types
- File size limits exceeded
- PDF processing failures
- Network connectivity issues
- Invalid questions or malformed requests

## 🔒 Security Considerations

- File type validation
- File size restrictions
- Input sanitization
- CORS configuration
- Rate limiting (recommended for production)

## 🚀 Deployment

### Production Deployment

1. **Backend Deployment:**
   ```bash
   # Using Docker
   docker build -t pdf-qa-backend .
   docker run -p 8000:8000 pdf-qa-backend
   
   # Or using gunicorn
   gunicorn main:app -w 4 -k uvicorn.workers.UvicornWorker
   ```

2. **Frontend Deployment:**
   ```bash
   npm run build
   # Deploy the build folder to your hosting service
   ```

### Environment-Specific Configurations
- Update API URLs for production
- Configure cloud storage for file uploads (AWS S3, Google Cloud Storage)
- Set up production database (PostgreSQL)
- Configure environment variables for production

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🆘 Support

If you encounter any issues or have questions:
1. Check the troubleshooting section below
2. Review the API documentation
3. Create an issue in the repository

## 🔧 Troubleshooting

### Common Issues

**PDF Upload Fails:**
- Check file size limits
- Ensure PDF is not corrupted
- Verify file permissions

**Questions Not Processing:**
- Verify OpenAI API key is set
- Check internet connectivity
- Ensure document was successfully processed

**Frontend Not Connecting to Backend:**
- Verify backend is running on port 8000
- Check CORS configuration
- Confirm API URL in frontend environment variables

### Logs
- Backend logs: Check console output from FastAPI server
- Frontend logs: Check browser developer console

## 📊 Monitoring

For production deployments, consider implementing:
- Application performance monitoring
- Error tracking (Sentry, Rollbar)
- Usage analytics
- Health check endpoints

---

**Project Volume Serial Number:** 5865-607D

**Last Updated:** May 2025

For more information or support, please refer to the project documentation or contact the development team.