# LlamaIndex GoogleGenAI Workflows

**Advanced AI workflows using enhanced GoogleGenAI features in LlamaIndex**

## 📓 Workflows

### 1. Lecture Q&A Chatbot (`lecture_qa_chatbot.ipynb`)

An intelligent academic assistant that processes lecture materials using **context caching** for efficient multi-turn conversations.

**Context Caching Architecture:**
- **File Upload**: PDF slides and MP3 audio uploaded to Google GenAI
- **Processing Wait**: Automatic waiting for file processing completion
- **Cache Creation**: 1-hour TTL cache containing both files with system instructions
- **Efficient Queries**: Subsequent questions use cached content without re-uploading

**Features:**
- **Dual Content Processing**: PDF lecture slides + audio recordings
- **Cost Optimization**: 50-90% API cost reduction through caching
- **Multi-turn Conversations**: Context preserved across questions
- **Expert Assistant**: System instruction for accurate academic responses
- **File State Management**: Automatic processing status checking

**Cache Configuration:**
```python
cache = client.caches.create(
    model="gemini-2.5-flash",
    config=CreateCachedContentConfig(
        display_name="Lecture Q&A Cache",
        system_instruction="Expert lecture assistant for accurate responses",
        contents=[
            Content(role="user", parts=[
                Part.from_uri(file_uri=pdf_file.uri, mime_type="application/pdf"),
                Part.from_uri(file_uri=audio_file.uri, mime_type="audio/mp3")
            ])
        ],
        ttl="3600s"  # 1 hour cache
    )
)
```

**Sample Queries:**
- Initial: "Summarize the key points from the lecture presentation and audio"
- Follow-up: "Explain the main concept discussed in slide 5 of the presentation"

**Use Cases:**
- Student study aids and lecture review
- Academic content analysis and summarization
- Educational Q&A systems
- Course material processing

### 2. Travel Itinerary Planner (`travel_itinerary_planner.ipynb`)

A comprehensive travel planning system using **multi-tool coordination** with 5 Google APIs for real-time information.

**Multi-API Integration:**
- **Google Gemini API**: LLM chat and intelligent tool calling
- **Google Geocoding API**: Location coordinate lookup
- **Google Routes API**: Distance and travel time calculations
- **Google Weather API**: Comprehensive weather forecasts
- **Google Time Zone API**: Accurate local time information

**Tool Calling Architecture:**
```python
# Real-time data tools
time_tool = FunctionTool.from_defaults(fn=get_current_time_wrapper)
weather_tool = FunctionTool.from_defaults(fn=get_weather_wrapper)  
distance_tool = FunctionTool.from_defaults(fn=calculate_distance_wrapper)

# Structured output model
class TravelItinerary(BaseModel):
    destination: str
    date: str
    items: List[ItineraryItem]  # time, activity, location, weather, travel_duration
```

**Intelligent Tool Orchestration:**
1. **Time Zone Detection**: Get current local time for destination
2. **Weather Integration**: Real-time weather forecasts for planning
3. **Distance Calculations**: Travel times between attractions
4. **Structured Generation**: Pydantic models for consistent output
5. **Multi-turn Refinement**: Follow-up queries to modify itineraries

**Sample Workflow:**
- Initial: "Generate a one-day travel itinerary for Paris with key activities, timings, weather, and travel durations"
- Follow-up: "Add a dinner reservation at a popular restaurant to the itinerary with travel duration"

**Use Cases:**
- Personalized trip planning with real-time data
- Business travel optimization
- Tourism itinerary generation
- Event planning with weather considerations

## 🔧 Setup

1. **Install Dependencies:**
   ```bash
   # Core LlamaIndex and GoogleGenAI integration
   pip install llama-index-llms-google-genai llama_index
   
   # For context caching and file upload (Lecture Q&A Chatbot)
   pip install google-generativeai
   
   # For data models and tool calling
   pip install pydantic
   
   # For API requests (Travel Itinerary Planner)
   pip install requests
   ```

2. **Google Cloud Console Setup** (for travel planner):
   - Enable: Geocoding API, Routes API, Weather API, Time Zone API
   - Create separate API keys for different service groups

## 📊 Performance Benefits

### Context Caching Advantages
- **Cost Reduction**: 50-90% lower API costs for repeated queries
- **Speed Improvement**: 2-3x faster response times
- **File Management**: Automatic processing and state tracking

### Multi-Tool Integration Benefits
- **Real-time Accuracy**: Always current information from multiple sources
- **Comprehensive Planning**: Weather, timing, and logistics in one workflow
- **Error Resilience**: Graceful handling of API failures

## 📋 Sample Data

- `sample_lecture_slides.pdf`: Academic presentation for Q&A testing
- `sample_lecture_audio.mp3`: Audio lecture for transcription examples

## 🔗 Resources

- [LlamaIndex GoogleGenAI Documentation](https://docs.llamaindex.ai/en/stable/examples/llm/google_genai/)
- [Google Cloud Console](https://console.cloud.google.com/) - Enable additional APIs
- [Gemini API Documentation](https://ai.google.dev/docs)

---

*Part of Google Summer of Code 2025 workflows*
