# Gemini API Workflow Examples

**Practical workflows demonstrating Gemini API capabilities in LangChain and LlamaIndex**

*Created as part of Google Summer of Code 2025*

## 🎯 Overview

This repository contains four comprehensive example workflows showcasing enhanced Gemini API integrations in LangChain and LlamaIndex. Each workflow demonstrates real-world applications using advanced features like multi-agent architecture, context caching, multi-tool coordination, and code execution.

## 📁 Workflows

### LangChain Examples
- **Grounded Search Agent**: Dual-agent architecture combining Google Search with PDF analysis for comprehensive research
- **Code Executing Chatbot**: Multi-turn conversations with dynamic Python code execution and visualization

### LlamaIndex Examples  
- **Lecture Q&A Chatbot**: Efficient document Q&A using context caching with PDF slides and audio lectures
- **Travel Itinerary Planner**: Multi-tool coordination using 5 Google APIs for real-time travel planning

## 🚀 Key Features Demonstrated

- **Dual-Agent Architecture**: Separate agents for search and synthesis to overcome API limitations
- **Context Caching**: 50-90% cost reduction for large document processing with 1-hour TTL
- **Multi-Tool Coordination**: Real-time integration with Google Search, Weather, Routes, and Time Zone APIs
- **Code Execution**: Dynamic Python code generation with matplotlib visualization and image output
- **Multimodal Processing**: PDF documents, audio files, and image handling
- **Structured Output**: Pydantic models for consistent, parseable responses

## 🔧 Quick Start

1. Choose a workflow from `LangChain/` or `LlamaIndex/` directory
2. Install dependencies: `pip install langchain-google-genai llama-index-llms-google-genai`
3. Set up your Google API keys (Gemini + additional Google services for some workflows)
4. Open notebooks in VS Code or Jupyter Lab and follow step-by-step instructions

## 📊 Sample Data Included

- `sample_sales_data.csv`: Sales data for code execution examples (200 rows)
- `sample.pdf`: Research document for grounded search agent
- `sample_lecture_slides.pdf`: Academic presentation for Q&A system
- `sample_lecture_audio.mp3`: Audio lecture for transcription workflow

## 🔗 Resources

- [Google AI Studio](https://aistudio.google.com/) - Get your Gemini API key
- [Gemini API Documentation](https://ai.google.dev/docs)
- [LangChain Google Integration](https://python.langchain.com/api_reference/google_genai/chat_models/langchain_google_genai.chat_models.ChatGoogleGenerativeAI.html)
- [LlamaIndex GoogleGenAI](https://docs.llamaindex.ai/en/stable/examples/llm/google_genai/)

---

*Part of Google Summer of Code 2025 - [Enhancing Gemini API Integrations in OSS Agent Tools](https://summerofcode.withgoogle.com/programs/2025/projects/GZnZhIEh)*
