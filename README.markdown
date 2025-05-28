# Musi-Chat: RAG-Based Musical Product Recommending QA Bot

![Musi-Chat Logo](link-to-logo.png) <!-- Replace with actual logo link if available -->

**Musi-Chat** is a domain-constrained Retrieval-Augmented Generation (RAG) chatbot designed to enhance the e-commerce experience for musical instrument enthusiasts. By leveraging the Amazon Reviews 2023 dataset, Musi-Chat provides precise, sentiment-aware responses to user queries about musical instruments, ensuring that answers are both detailed and relevant. The chatbot is integrated into an Amazon-like front-end interface, offering an intuitive and familiar user experience.

## Table of Contents
- [Introduction](#introduction)
- [Key Features](#key-features)
- [Technologies Used](#technologies-used)
- [Setup Instructions](#setup-instructions)
- [Usage](#usage)
- [Known Issues](#known-issues)
- [Contributing](#contributing)
- [License](#license)

## Introduction
Musi-Chat addresses the challenges of information overload and imprecise responses in e-commerce by providing a conversational AI tailored to musical instruments. It combines retrieval and generation techniques to deliver accurate, contextually relevant answers while gracefully handling off-topic queries. The project demonstrates the practical application of RAG in a specialized domain, setting a foundation for scalable, domain-specific chatbots in online retail.

## Key Features
- **Domain-Constrained Responses**: Ensures answers are strictly related to musical instruments, with a 95% accuracy in rejecting off-topic queries.
- **Sentiment-Aware Insights**: Integrates fine-tuned DistilBERT to provide empathetic responses based on user reviews.
- **Efficient Retrieval**: Uses FAISS with HNSW indexing and MMR for fast, relevant document retrieval.
- **Scalable Architecture**: Designed for adaptability to other e-commerce domains (e.g., electronics, books).
- **Real-Time Performance**: Delivers responses within 2–3 seconds, ensuring a seamless user experience.

## Technologies Used
- **Programming Language**: Python
- **NLP Models**: DistilBERT (sentiment analysis), `all-MiniLM-L6-v2` (embeddings), `phi` LLM (generation)
- **Retrieval**: FAISS, HNSW indexing, MMR
- **Frameworks**: LangChain (RAG pipeline), FastAPI (backend), PyTorch (training)
- **Front-End**: HTML, CSS, JavaScript (Amazon-like interface)
- **Tools**: ngrok (tunneling), Sentence-Transformers, Ollama

## Setup Instructions
To set up Musi-Chat locally, follow these steps:

### Prerequisites
- Python 3.8+
- Git
- Google Colab or a local environment with GPU support (for training)
- ngrok account (for front-end tunneling)

### Installation
1. **Clone the Repository**:
   ```bash
   git clone https://github.com/your-username/musi-chat.git
   cd musi-chat
   ```

2. **Install Dependencies**:
   ```bash
   pip install -r requirements.txt
   ```
   *Note: Ensure `requirements.txt` includes all necessary packages (e.g., `transformers`, `sentence-transformers`, `faiss-cpu`, `langchain`, `fastapi`, `torch`).*

3. **Download Datasets**:
   - Amazon Reviews 2023 (Musical Instruments): [Link to dataset](https://example.com/amazon-reviews-2023)
   - Kaggle Amazon Reviews: [Link to dataset](https://www.kaggle.com/datasets/bittlingmayer/amazonreviews)

4. **Preprocess Data**:
   - Run `preprocess.py` to clean, filter, and label the datasets.
   ```bash
   python preprocess.py --input amazon_reviews_2023.json --output final_dataset.json
   ```

5. **Fine-Tune DistilBERT**:
   - Use `finetune_distilbert.py` with the Kaggle dataset.
   ```bash
   python finetune_distilbert.py --train_data train.csv --val_data test.csv
   ```

6. **Set Up RAG Pipeline**:
   - Embed documents using `embed_documents.py`.
   - Build FAISS index with `build_index.py`.

7. **Run the Backend**:
   - Start the FastAPI server.
   ```bash
   uvicorn app:app --host 0.0.0.0 --port 8000
   ```

8. **Set Up Front-End**:
   - Run the front-end server or open `index.html` in a browser.
   - Use ngrok to tunnel the backend:
   ```bash
   ngrok http 8000
   ```

## Usage
- **Query the Chatbot**: Enter queries like "Tell me about the Yamaha YFL-222 flute" or "Are customers happy with the Fender Stratocaster?" in the front-end modal.
- **Off-Topic Queries**: Non-product queries (e.g., "What is a black hole?") will receive a fallback response: "Sorry, I can only assist with product queries."

## Known Issues
- **Edge-Case Misclassification**: Queries with semantic overlap (e.g., "sound wave") may occasionally be misclassified as product-related.
- **Fixed Response Length**: Responses are limited to 150–200 tokens, which may not suit all query complexities.
- **Computational Constraints**: Training and embedding steps require significant GPU resources; use Google Colab or a similar environment.

## Contributing
We welcome contributions to enhance Musi-Chat! To contribute:
1. Fork the repository.
2. Create a new branch (`git checkout -b feature/your-feature`).
3. Commit your changes (`git commit -m 'Add your feature'`).
4. Push to the branch (`git push origin feature/your-feature`).
5. Open a pull request.

Please ensure your contributions align with the project’s goals and include clear documentation.

To view the clear description of project file [Click here](https://www.notion.so/Musi-chat-RAG-based-Musical-Product-Recommending-QA-Bot-1dfedc93806d80699b24d624c72aa603?pvs=4)  
To access the datasets [Click here](https://drive.google.com/drive/u/2/folders/1lKhWzSr_8UbmAqJZU3ybIjI0YMSXUxYP)
