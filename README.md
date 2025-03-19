# Medical-RAG-using-Bio-Mistral-7B
This is a RAG implementation using Open Source stack. BioMistral 7B has been used to build this app along with PubMedBert as an embedding model, Qdrant as a self hosted Vector DB, and Langchain &amp; Llama CPP as an orchestration frameworks.
## Implementation on Intel AI PC    
### Disclaimer   
This demo is intended only for the purpose of exploring new LLM use cases at the edge and not recommended for production-grade medical chatbot    

### Device Under Test   
Processor: Intel® Core™ Ultra 7 165H      
OS: Windows 11 Pro 23H2   
RAM: 64GB   
Python 3.11.9   

### Prerequisite   
Install [Microsoft Visual C++](https://code.visualstudio.com/docs/cpp/config-msvc) compiler toolset required for installing llama-cpp-python       

### Steps   
1. Clone this repository
2. Create a Python virtual environment and install the dependencies   
   ```
   python -m venv biomistral_rag   
   biomistral_rag\Scripts\activate   
   python -m pip install pip --upgrade  
   cd Medical-RAG-using-Bio-Mistral-7B-main
   pip install -r requirements.txt   
   pip install qdrant-client --upgrade   
   ```
3. Download the INT4 version of [BioMistral-7B](https://huggingface.co/MaziyarPanahi/BioMistral-7B-GGUF/blob/main/BioMistral-7B.Q4_K_M.gguf) model in GGUF format 
4. Download the embedding model
   ```
   git lfs install
   git clone https://huggingface.co/NeuML/pubmedbert-base-embeddings
   ```
5. Install [Docker Desktop for Windows](https://docs.docker.com/desktop/setup/install/windows-install/) with optional proxy settings    
6. Create the Qdrant container
   ```
   docker pull qdrant/qdrant
   docker run -p 6333:6333 -v .\qdrant_db\:/qdrant/storage qdrant/qdrant
   ```
   ![image](https://github.com/user-attachments/assets/36b17d09-2f61-4645-a336-3458627da6be)   
   Access the Dashboard using http://localhost:6333/dashboard    
7. Create embeddings for the new documents in data
   ```
   python ingest.py
   ```   
   Check the new Collection on the Qdrant Dashboard   
   ![image](https://github.com/user-attachments/assets/13740e55-4e12-4d0f-8267-695d5edeec0a)     
8. Run the application
   ```
   uvicorn app:app   
   ```
   ![image](https://github.com/user-attachments/assets/5ec90875-be78-4bc9-9acf-09859235e313)    
#### Sample Outputs
![image](https://github.com/user-attachments/assets/94282267-ebf0-46eb-b587-996e886e6cb7)   
![image](https://github.com/user-attachments/assets/37aa70b3-1b6d-49b3-a050-d6d5aef882ee)   
