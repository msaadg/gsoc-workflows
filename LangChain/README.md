# LangChain Gemini Workflows

**Advanced AI workflows using enhanced Gemini API features in LangChain**

## 📓 Workflows

### 1. Grounded Search Agent (`grounded_search_agent.ipynb`)

A sophisticated **dual-agent research system** that combines real-time Google Search with PDF document analysis.

**Architecture:**
- **Search Agent**: Uses Google Search grounding to gather current web information
- **Synthesis Agent**: Processes search results + PDF content into structured responses
- **Separation Strategy**: Overcomes API limitations by separating tool usage from structured output

**Features:**
- Multi-document PDF processing with base64 encoding
- Real-time Google Search integration with source attribution
- Structured JSON output using comprehensive Pydantic models
- Two-step workflow: search → synthesis for optimal performance

**Output Structure:**
```python
class ResearchResponse(BaseModel):
    query: str
    answer: ResearchAnswer  # summary, analysis, findings, conclusion
    search_insights: List[SearchInsight]  # findings with source URLs
    file_insights: List[FileInsight]  # PDF analysis with relevance
    synthesis: str  # Integration of all sources
```

**Use Cases:**
- Academic research combining current literature with course materials
- Business intelligence with market research + internal documents
- Technical research merging latest frameworks with existing documentation

### 2. Code Executing Chatbot (`code_executing_chatbot.ipynb`)

An interactive data analysis assistant that executes Python code and generates visualizations through multi-turn conversations.

**Features:**
- **Dynamic Code Execution**: Real-time Python code generation and execution
- **Visualization Support**: Matplotlib charts with inline display and PNG file saving
- **Context Preservation**: Multi-turn conversations maintaining data analysis state
- **CSV Processing**: Efficient handling of 200-row datasets for faster processing
- **Dual Output**: Images displayed inline + saved as files

**Workflow Process:**
1. Load CSV data and embed in conversation context
2. Process initial analysis query with code execution
3. Display generated charts inline and save as PNG files
4. Handle follow-up queries with preserved conversation context
5. Iterative refinement of visualizations based on feedback

**Sample Workflow:**
```python
# Initial: "Analyze sales trends and plot monthly sales as a line chart"
# Follow-up: "Highlight the top-performing months in red on the chart"
```

**Use Cases:**
- Business intelligence dashboards
- Educational data science learning
- Financial analysis and reporting
- Marketing analytics with visual insights

## 🔧 Setup

1. **Install Dependencies:**
   ```bash
   # Core LangChain and Gemini integration
   pip install langchain-google-genai langchain-core
   
   # For structured output and data models
   pip install pydantic
   
   # For data analysis and visualization (Code Executing Chatbot)
   pip install pandas matplotlib pillow
   
   # For notebook display (if using Jupyter)
   pip install ipython
   ```

2. **Prepare Data:**
   - Place CSV files for analysis in the same directory
   - Ensure PDF documents are accessible for research workflows

## 🛠 Technical Implementation

### Dual-Agent Architecture
```python
# Search Agent (with tools, no structured output)
search_llm = ChatGoogleGenerativeAI(model="gemini-2.5-flash")
response = search_llm.invoke([message], tools=[GenAITool(google_search={})])

# Synthesis Agent (structured output, no tools)
synthesis_llm = ChatGoogleGenerativeAI(model="gemini-2.5-flash")
structured_llm = synthesis_llm.with_structured_output(ResearchResponse, method="json_mode")
```

### Code Execution with Context
```python
# Multi-turn conversation with preserved context
llm = ChatGoogleGenerativeAI(model="gemini-2.5-flash").bind_tools([{"code_execution": {}}])

# Add AI responses to conversation history for context
messages.append(AIMessage(content=initial_response.content))
follow_up_response = llm.invoke(messages)
```

### Multimodal PDF Processing
```python
# Base64 encode PDFs for AI processing
def load_pdf_as_base64(pdf_path: str) -> str:
    with open(pdf_path, 'rb') as file:
        pdf_bytes = file.read()
    return base64.b64encode(pdf_bytes).decode('utf-8')

# Embed in message content
content.append({
    "type": "file",
    "source_type": "base64", 
    "mime_type": "application/pdf",
    "data": pdf_base64
})
```

## 📊 Sample Data

- `sample_sales_data.csv`: Kaggle sales dataset (200 rows) for code execution examples
- `sample.pdf`: Research document for grounded search demonstrations

## 🔗 Resources

- [LangChain Google Integration](https://python.langchain.com/api_reference/google_genai/chat_models/langchain_google_genai.chat_models.ChatGoogleGenerativeAI.html)
- [Gemini API Documentation](https://ai.google.dev/docs)
- [Google AI Studio](https://aistudio.google.com/)

---

*Part of Google Summer of Code 2025 workflows*
