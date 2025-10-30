# Flood Detection API

A FastAPI-based backend service for flood risk assessment using Google's Gemini AI. This API analyzes terrain images to provide flood risk assessments, elevation estimates, and safety recommendations.

## Features

- **Image Analysis**: Upload terrain images for flood risk assessment
- **AI-Powered**: Uses Google Gemini 2.0 Flash for intelligent analysis
- **Real-time Processing**: Fast analysis with detailed risk reports
- **RESTful API**: Clean, documented endpoints
- **CORS Enabled**: Ready for web applications

## Quick Start

### Prerequisites

- Python 3.8+
- Google Gemini API key

### Installation

1. Clone the repository:

   ```bash
   git clone <repository-url>
   cd 1st-fastapi-app-be
   ```

2. Create a virtual environment:

   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

4. Set up environment variables:

   Create a `.env` file in the root directory:

   ```bash
   GEMINI_API_KEY=your_gemini_api_key_here
   ```

### Running the Application

Use the provided startup script:

```bash
python start.py
```

Or run directly:

```bash
uvicorn main:app --reload
```

The API will be available at `http://localhost:8000`

## API Documentation

### Interactive Documentation

Once the server is running, you can access the interactive API documentation:

- **Swagger UI**: `http://localhost:8000/docs`
- **ReDoc**: `http://localhost:8000/redoc`
- **OpenAPI JSON**: `http://localhost:8000/openapi.json`

### API Endpoints

#### Health Check Endpoints

**GET /** - Basic health check

- Returns API status and version information

**GET /health** - Detailed health check

- Returns detailed health status including AI model information

#### Analysis Endpoints

**POST /api/analyze/image** - Analyze flood risk from image

- **Input**: Image file (max 10MB, image/* content type)
- **Output**: Comprehensive flood risk assessment

##### Request

- Method: `POST`
- Content-Type: `multipart/form-data`
- Body: `file` parameter with image file

##### Response

```json
{
  "success": true,
  "risk_level": "Medium",
  "description": "Analysis completed",
  "recommendations": [
    "Monitor weather conditions",
    "Stay informed about local alerts"
  ],
  "elevation": 50.0,
  "distance_from_water": 1000.0,
  "ai_analysis": "Detailed AI analysis of the image",
  "message": "Image analysis completed successfully using Gemini AI"
}
```

##### Risk Levels

- **Low**: Minimal flood risk
- **Medium**: Moderate risk requiring monitoring
- **High**: Significant risk requiring protective measures
- **Very High**: Critical risk requiring immediate action

## Configuration

### Environment Variables

- `GEMINI_API_KEY`: Your Google Gemini API key (required)
- `PORT`: Server port (default: 8000)
- `HOST`: Server host (default: 0.0.0.0)

### File Upload Limits

- Maximum file size: 10MB
- Supported formats: All common image formats (JPEG, PNG, GIF, etc.)

## Error Handling

The API returns appropriate HTTP status codes:

- `200`: Success
- `400`: Bad request (invalid file, size limit exceeded)
- `500`: Internal server error

Error responses include a `detail` field with error description.

## Dependencies

Key dependencies include:

- **FastAPI**: Modern web framework
- **Uvicorn**: ASGI server
- **Google Generative AI**: Gemini AI integration
- **Pillow**: Image processing
- **Pydantic**: Data validation

See `requirements.txt` for complete list.

## Development

### Project Structure

```text
├── main.py          # Main FastAPI application
├── start.py         # Startup script
├── requirements.txt # Python dependencies
├── runtime.txt      # Python version specification
├── .env            # Environment variables (not in repo)
└── README.md       # This file
```

### Running Tests

```bash
# Add tests here when implemented
```

## Deployment

### Local Deployment

Follow the installation and running instructions above.

### Production Deployment

1. Set environment variables securely
2. Use a production ASGI server (e.g., Gunicorn + Uvicorn workers)
3. Configure reverse proxy (nginx recommended)
4. Enable HTTPS
5. Set appropriate file upload limits

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## Support

For issues and questions:

- Check the API documentation at `/docs`
- Review the logs for error details
- Ensure your Gemini API key is valid and has sufficient quota
