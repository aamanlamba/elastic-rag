# Elasticsearch RAG with AWS Bedrock and LangChain

This project demonstrates how to build a Retrieval-Augmented Generation (RAG) system using Elasticsearch as the vector store, AWS Bedrock for embeddings, and LangChain for the integration layer.

## Prerequisites

- Python 3.x with virtual environment
- AWS account with Bedrock access
- Elastic Cloud account (or Elasticsearch instance)
- Required Python packages (installed via `requirements.txt`):
  - langchain-elasticsearch
  - langchain-aws
  - python-dotenv
  - boto3
  - tiktoken

## Environment Setup

1. Clone this repository
2. Create and activate a virtual environment:

   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows use: .\venv\Scripts\activate
   ```

3. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

4. Create a `.env` file in the project root with your credentials:

   ```env
   ELASTIC_CLOUD_ENDPOINT=your_elasticsearch_endpoint
   ELASTIC_API_KEY=your_elasticsearch_api_key
   AWS_ACCESS_KEY=your_aws_access_key
   AWS_SECRET_KEY=your_aws_secret_key
   AWS_REGION=your_aws_region
   ELASTIC_CLOUD_ID=your_elastic_cloud_id  # Optional
   ```

## Running the Notebook

The `rag_setup.ipynb` notebook walks through:

1. Setting up connections to AWS Bedrock and Elasticsearch
2. Loading sample workplace documents from a JSON file
3. Creating text chunks with RecursiveCharacterTextSplitter
4. Generating embeddings using AWS Bedrock's Titan model
5. Storing documents and embeddings in Elasticsearch
6. (Optional) Testing document retrieval

Important Notes:

- Make sure to use an embedding-capable model ID for AWS Bedrock (e.g., `amazon.titan-embed-text-v2:0`)
- The notebook uses the Elastic Labs sample data for demonstration
- Text chunks are configured for 512 tokens with 256 token overlap

## Key Components

- **AWS Bedrock**: Provides the embedding model (Titan) for converting text into vectors
- **Elasticsearch**: Stores documents and vectors, enables semantic search
- **LangChain**: Orchestrates the RAG workflow and provides helper classes
- **Text Splitter**: Breaks documents into chunks suitable for embedding

## Common Issues

1. **Embedding Errors**: Ensure you're using an embedding-specific model ID (e.g., `amazon.titan-embed-text-v2:0`) rather than a text generation model
2. **Authentication**: Double-check your AWS and Elasticsearch credentials in the `.env` file
3. **Missing Dependencies**: Run `pip install -r requirements.txt` with your virtual environment activated

## Useful Commands

Check AWS Bedrock access:

```python
import boto3
client = boto3.client('bedrock-runtime', region_name='your-region')
# If no error, connection is good
```

Test Elasticsearch connection:

```python
from langchain_elasticsearch import ElasticsearchStore
# If vector_store instantiates without error, connection is good
```

## Resources

- [Elasticsearch Vector Search Documentation](https://www.elastic.co/guide/en/elasticsearch/reference/current/vector-search.html)
- [AWS Bedrock Developer Guide](https://docs.aws.amazon.com/bedrock/)
- [LangChain Documentation](https://python.langchain.com/docs/get_started/introduction)

## License

MIT License - feel free to use and modify for your own projects.
