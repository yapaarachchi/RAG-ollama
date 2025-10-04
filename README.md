# RAG-Ollama: Restaurant Review Q&A System

A Retrieval-Augmented Generation (RAG) system that uses Ollama and LangChain to answer questions about restaurant reviews. This project demonstrates how to build a local RAG system using open-source tools for document retrieval and question answering.

## Project Description

This project creates an intelligent Q&A system for restaurant reviews using:
- **RAG Architecture**: Combines document retrieval with language generation
- **Local LLM**: Uses Ollama with Llama 3.2 model for responses
- **Vector Database**: ChromaDB for efficient similarity search
- **Embeddings**: mxbai-embed-large model for document embeddings

The system allows users to ask questions about restaurant reviews and get contextual answers based on the most relevant review content.

## Tools and Technologies Used

- **Python 3.13**
- **LangChain**: Framework for building LLM applications
- **LangChain-Ollama**: Integration for local Ollama models
- **LangChain-Chroma**: Vector database integration
- **Ollama**: Local LLM server
- **ChromaDB**: Vector database for embeddings
- **Pandas**: Data manipulation
- **mxbai-embed-large**: Embedding model for text vectorization
- **llama3.2**: Language model for text generation

## Prerequisites

Before setting up the project, ensure you have:

1. **Python 3.13** installed
2. **Ollama** installed and running locally
3. **Git** (for cloning the repository)

## Setup Instructions

### 1. Clone the Repository

```bash
git clone <your-repo-url>
cd RAG-ollama
```

### 2. Install Ollama

#### macOS (using Homebrew)
```bash
brew install ollama
```

#### Linux
```bash
curl -fsSL https://ollama.ai/install.sh | sh
```

#### Windows
Download the installer from [ollama.ai](https://ollama.ai/download)

### 3. Start Ollama Service

```bash
ollama serve
```

### 4. Pull Required Models

In a new terminal window, pull the required models:

```bash
# Pull the language model
ollama pull llama3.2

# Pull the embedding model
ollama pull mxbai-embed-large
```

### 5. Create Virtual Environment

```bash
python -m venv myenv
```

### 6. Activate Virtual Environment

#### macOS/Linux
```bash
source myenv/bin/activate
```

#### Windows
```bash
myenv\Scripts\activate
```

### 7. Install Dependencies

```bash
pip install -r requirements.txt
```

## Running the Application

### 1. Ensure Ollama is Running

Make sure Ollama service is running in the background:

```bash
ollama serve
```

### 2. Run the Application

```bash
python main.py
```

### 3. Interact with the System

Once the application starts, you can ask questions about the restaurant reviews. For example:

- "What do customers say about the pizza quality?"
- "Are there any complaints about delivery service?"
- "What are the best-rated aspects of this restaurant?"
- "Do they have gluten-free options?"

Type `q` to quit the application.

## Project Structure

```
RAG-ollama/
├── main.py                              # Main application entry point
├── vector.py                            # Vector database setup and retrieval logic
├── requirements.txt                     # Python dependencies
├── realistic_restaurant_reviews.csv     # Restaurant review dataset
├── books.csv                           # Additional dataset (not used in main app)
├── chrome_langchain_db/                # ChromaDB persistence directory
│   ├── chroma.sqlite3                  # Database file
│   └── [collection files]              # Vector embeddings
├── myenv/                              # Python virtual environment
└── README.md                           # This file
```

## How It Works

1. **Data Processing**: Restaurant reviews are loaded from CSV and converted into documents
2. **Embedding Generation**: Each review is converted to vector embeddings using mxbai-embed-large
3. **Vector Storage**: Embeddings are stored in ChromaDB for efficient similarity search
4. **Query Processing**: User questions are converted to embeddings
5. **Retrieval**: Most relevant reviews are retrieved based on semantic similarity
6. **Generation**: Retrieved context is passed to Llama 3.2 model for answer generation

## Customization

### Adding New Data

To use your own review data:

1. Replace `realistic_restaurant_reviews.csv` with your data
2. Ensure your CSV has columns: `Title`, `Date`, `Rating`, `Review`
3. Delete the `chrome_langchain_db` directory to rebuild the vector database
4. Run the application - it will automatically process the new data

### Changing Models

To use different models, modify the model names in:

- `main.py`: Change `model="llama3.2"` to your preferred LLM
- `vector.py`: Change `model="mxbai-embed-large"` to your preferred embedding model

Make sure to pull the new models with Ollama first:

```bash
ollama pull <your-model-name>
```

## Troubleshooting

### Common Issues

1. **"Connection refused" error**: Ensure Ollama service is running (`ollama serve`)
2. **Model not found**: Pull the required models with `ollama pull <model-name>`
3. **Permission errors**: Make sure you have write permissions in the project directory
4. **Memory issues**: Large models require sufficient RAM (8GB+ recommended)

### Performance Tips

- Use smaller models for faster responses
- Reduce the number of retrieved documents (`k` parameter in `vector.py`)
- Consider using GPU acceleration if available

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## License

This project is open source and available under the MIT License.

## Acknowledgments

- [Ollama](https://ollama.ai/) for providing local LLM capabilities
- [LangChain](https://langchain.com/) for the RAG framework
- [ChromaDB](https://www.trychroma.com/) for vector storage
