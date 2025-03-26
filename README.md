## Semantic search

In this guide we'll learn sematic search through Redis vector DB. Semantic search extends traditional database search methods to interpret the user's query and extract the documents that match the semantic meaning of the query. With the semantic search features, it is possible to query the database in natural language: it understands the semantics behind the query and returns meaningful results. 

Semantic similarity is achieved by generating a vectors that represents the features of the data under analysis because the vector is a convenient data structure to compress information and is easily manageable by a computer. Vectors are lists of floating point numbers that represent features of unstructured data that play a massive role in Machine Learning.

## How to obtain vectors
Vectors represent unstructured data and are essentially lists of decimal numbers. When vectors are used in semantic search, we refer to vector embeddings. The term "embedding" helps reflect the transformation of data to a lower-dimensional space while preserving the features of the original data, so the vector embeds the structures and relationships of the original data which may be the semantic meaning of a paragraph or the attributes like colors, angles, lines, and shapes in a picture, and so on. 

Embedding models translate the human-perceived semantic similarity to the vector space. 
Example- 
Github Market place have hosted models which we could try free of cost. All it needs is a github account.
![Embedding Models on GitHub Marketplace](github_embedding_models.png)

Output embedding dimesions for the above models - 
| Model Name                        | Output Embedding Dimension |
|-----------------------------------|----------------------------|
| Cohere Embed v3 Multilingual      | 1024                       |
| Cohere Embed v3 English           | 1024                       |
| OpenAI Text Embedding 3 (small)   | 1536                       |
| OpenAI Text Embedding 3 (large)   | 3072                       |

When a machine learning model generates vectors, they embed the distinctive features of data into floating point numbers of fixed size in a compact and dense representation and translate the human-perceived semantic similarity to the vector space. The semantic similarity of two objects (two texts expressing the same concepts and overall meaning or two similar pictures) translates to the "numerical similarity" of two vectors, which is calculated as the distance between vectors, a simple mathematical operation.

Comparisons between vectors occur in the same vector space, where the vectors must have the same size. Therefore, ensure that your data is embedded for ingestion and semantic search prompts using the same embedding model.
To get started, set up a Python virtual environment to isolate the required packages for your testing. This ensures a clean and manageable workspace. You can create and activate a virtual environment using the following commands:

```bash
# Create a virtual environment
python -m venv .venv

# Activate the virtual environment
# On Windows
env\Scripts\activate
# On macOS/Linux
source env/bin/activate
```

Once the virtual environment is activated, install the necessary packages using `pip`:

```bash
pip install -r requirements.txt
```

## Install Redis Stack on Docker to test out semantic search 

https://redis.io/docs/latest/operate/oss_and_stack/install/install-stack/docker/

redis/redis-stack contains both Redis Stack server and Redis Insight. This container is best for local development because you can use the embedded Redis Insight to visualize your data.

To start a Redis Stack container using the redis-stack image, with persistent volume, run the below command

```bash
docker run -d --name redis-stack -p 6379:6379 -p 8001:8001 -v /Users/rashmikare/Learn/Repos/MyRepos/data:/data redis/redis-stack:latest
```

The docker run command above also exposes Redis Insight on port 8001. You can use Redis Insight by pointing your browser to localhost:8001.