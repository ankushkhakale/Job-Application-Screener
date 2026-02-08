# 🎯 AI-Powered Job Application Screener

## The Story Behind the Project

In today's competitive job market, recruiters and hiring managers face an overwhelming challenge: sorting through hundreds of applications to find the perfect candidate. Each resume tells a story, but with limited time, many qualified candidates might be overlooked. This is where the AI-Powered Job Application Screener comes into play.

Born from the need to make hiring more efficient and fair, this project harnesses the power of artificial intelligence to transform the candidate screening process. By combining modern AI technology with an intuitive user interface, we've created a tool that helps recruiters make informed decisions quickly while ensuring no qualified candidate falls through the cracks.

## What It Does

The Job Application Screener is an intelligent assistant that bridges the gap between job requirements and candidate qualifications. At its core, it's a web-based application that analyzes resumes against job descriptions, providing detailed insights that help recruiters make better hiring decisions.

The system works by:
- **Understanding Context**: It reads and comprehends both the resume content and job requirements
- **Intelligent Matching**: Using DeepSeek AI, it identifies skill matches, experience alignments, and potential gaps
- **Scoring Candidates**: It provides a suitability score (0-100%) based on qualifications and experience
- **Highlighting Insights**: It pinpoints exact matches and clearly indicates missing criteria

## ✨ Features

### Current Capabilities

- **🤖 AI-Powered Analysis**: Leverages DeepSeek-R1 model for deep understanding of resumes and job descriptions
- **📊 Suitability Scoring**: Provides quantitative scores to help rank candidates objectively
- **🎨 User-Friendly Interface**: Built with Gradio for a clean, intuitive web interface
- **📝 Detailed Reports**: Generates comprehensive screening reports highlighting strengths and gaps
- **⚡ Fast API Backend**: Alternative FastAPI endpoint for programmatic access
- **🔍 Smart Comparison**: Identifies skill matches and missing qualifications automatically

### How It Helps

For recruiters, this means:
- Spending less time on initial screening
- Making more objective hiring decisions
- Identifying promising candidates who might otherwise be missed
- Having clear, documented reasons for candidate selection

## 🛠️ Prerequisites

Before embarking on your journey with this application, you'll need a few tools in your toolkit:

### Required Software

1. **Python 3.8 or higher**: The language that powers our application
2. **Ollama**: The local AI engine that runs DeepSeek models
3. **DeepSeek-R1 Model**: The AI brain that analyzes resumes

### Python Dependencies

The application relies on these carefully selected libraries:
- `gradio`: Creates the beautiful web interface
- `fastapi`: Powers the API backend
- `requests`: Handles communication with the AI model
- `PyMuPDF (fitz)`: Extracts text from PDF resumes
- `uvicorn`: Runs the FastAPI server

## 📦 Installation

Let's get you up and running! Follow this journey step by step:

### Step 1: Setting Up Ollama

First, we need to set up the AI engine:

```bash
# Install Ollama (visit https://ollama.ai for your OS-specific instructions)
# For Linux:
curl -fsSL https://ollama.ai/install.sh | sh

# Pull the DeepSeek-R1 model
ollama pull deepseek-r1

# Start Ollama server (it should run on localhost:11434)
ollama serve
```

### Step 2: Clone the Repository

Bring the project to your local machine:

```bash
git clone https://github.com/ankushkhakale/Job-Application-Screener.git
cd Job-Application-Screener
```

### Step 3: Install Python Dependencies

Set up the Python environment:

```bash
# Optional but recommended: Create a virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install required packages
pip install gradio fastapi requests pymupdf uvicorn
```

### Step 4: Verify Installation

Make sure Ollama is running and accessible:

```bash
curl http://localhost:11434/api/generate -d '{
  "model": "deepseek-r1",
  "prompt": "Hello",
  "stream": false
}'
```

If you see a response, you're ready to go!

## 🚀 Usage

The application offers two ways to interact with it, each designed for different use cases:

### Option 1: Gradio Web Interface (Recommended for Beginners)

This is the most intuitive way to use the screener. Perfect for recruiters who want a visual interface:

```bash
python job_screener.py
```

Once launched, your browser will open to a friendly interface where you can:

1. **Enter Candidate Information**: Paste the resume text or candidate details in the first text box
2. **Provide Job Description**: Paste the complete job description in the second text box
3. **Click Submit**: Watch as the AI analyzes and generates a detailed report
4. **Review Results**: Read the suitability score, matched skills, and recommendations

**Example Usage:**

*Candidate Information:*
```
Name: Sarah Johnson
Experience: 5 years in Full-Stack Development
Skills: Python, JavaScript, React, Node.js, MongoDB, AWS
Education: B.Sc. in Computer Science
Previous Role: Senior Developer at Tech Startup
```

*Job Description:*
```
Role: Senior Full-Stack Engineer
Required Skills: Python, React, Node.js, Docker, AWS
Experience: 3+ years in web development
Responsibilities: Building scalable web applications, API development, cloud deployment
```

The AI will then provide a detailed analysis with a suitability score and specific insights.

### Option 2: FastAPI Backend (For Developers)

If you're building an automated system or need programmatic access:

```bash
uvicorn app:app --reload
```

Access the API at `http://localhost:8000`. The interactive API documentation is available at `http://localhost:8000/docs`.

**API Endpoint:**

```bash
POST /screen_candidate/
Content-Type: application/json

{
  "resume": "Your resume text here...",
  "job_description": "Your job description here..."
}
```

**Example with curl:**

```bash
curl -X POST "http://localhost:8000/screen_candidate/" \
  -H "Content-Type: application/json" \
  -d '{
    "resume": "John Doe, 3 years Python development...",
    "job_description": "Looking for Python developer with 2+ years..."
  }'
```

## 📁 Project Structure

Understanding the architecture helps you navigate and contribute:

```
Job-Application-Screener/
│
├── job_screener.py          # Main Gradio application
│   ├── extract_text_from_pdf()  # PDF text extraction (ready for future use)
│   ├── screen_candidate()       # Core AI screening logic
│   └── Gradio Interface         # Web UI definition
│
├── app.py                   # FastAPI backend
│   └── /screen_candidate/       # API endpoint for screening
│
└── README.md                # You are here!
```

### Key Components Explained

**job_screener.py**: This is the heart of the user-facing application. It creates a beautiful web interface using Gradio and handles the interaction between users and the AI model. The code is structured to be easily extensible—notice the commented-out PDF extraction function, ready for future enhancements.

**app.py**: A lightweight FastAPI application that provides a RESTful API interface. Perfect for integrating the screener into existing HR systems or building custom workflows.

## 🔧 Technical Details

### The AI Engine

The application uses **DeepSeek-R1**, a powerful language model running locally through Ollama. This choice offers several advantages:
- **Privacy**: All data stays on your machine—no resume information leaves your infrastructure
- **Speed**: Local processing means fast responses
- **Cost-Effective**: No API costs or rate limits
- **Customizable**: You can fine-tune the model for specific industries

### Communication Flow

```
User Input → Gradio/FastAPI → HTTP Request → Ollama (localhost:11434) → DeepSeek-R1 → Analysis → Response
```

The prompt engineering is carefully designed to:
1. Understand both resume and job description context
2. Extract relevant skills and experience
3. Compare qualifications against requirements
4. Generate a structured suitability score
5. Highlight matches and identify gaps

## 🌟 Future Enhancements

The journey doesn't end here. Here are exciting features on the roadmap:

### Planned Features

- **📄 PDF Upload Support**: Direct PDF resume upload (foundation already in place)
- **📊 Batch Processing**: Screen multiple candidates simultaneously
- **💾 Database Integration**: Store and compare historical screenings
- **📈 Analytics Dashboard**: Visualize hiring trends and candidate pools
- **🎯 Custom Scoring Models**: Industry-specific evaluation criteria
- **🔄 Interview Question Generation**: Automatic creation of tailored interview questions
- **📧 Email Integration**: Direct candidate communication from the platform
- **🌍 Multi-Language Support**: Analyze resumes in different languages

## 🤝 Contributing

We believe in the power of community! If you'd like to contribute to making hiring fairer and more efficient:

1. **Fork the Repository**: Create your own copy
2. **Create a Feature Branch**: `git checkout -b feature/AmazingFeature`
3. **Make Your Changes**: Add your improvements
4. **Test Thoroughly**: Ensure everything works
5. **Commit Your Changes**: `git commit -m 'Add some AmazingFeature'`
6. **Push to Branch**: `git push origin feature/AmazingFeature`
7. **Open a Pull Request**: Share your contribution

### Areas We'd Love Help With

- PDF extraction improvements
- Additional AI model integrations
- UI/UX enhancements
- Documentation and tutorials
- Performance optimizations
- Test coverage

## ⚖️ License

This project is open source and available for use in both personal and commercial applications.

## 🙏 Acknowledgments

- **Ollama Team**: For making local AI accessible
- **DeepSeek**: For the powerful language model
- **Gradio**: For the amazing UI framework
- **FastAPI**: For the elegant API framework
- **The Open Source Community**: For inspiration and support

## 📞 Support & Contact

If you encounter any issues or have questions:
- Open an issue in the GitHub repository
- Reach out to the maintainer: [ankushkhakale](https://github.com/ankushkhakale)

## 🎓 Learn More

Interested in the technology behind this project?
- [Ollama Documentation](https://ollama.ai)
- [Gradio Documentation](https://gradio.app)
- [FastAPI Documentation](https://fastapi.tiangolo.com)

---

**Built with ❤️ to make hiring more efficient, fair, and human.**

*Remember: While AI is a powerful tool, it should augment human decision-making, not replace it. Always review AI recommendations with human judgment and empathy.*
