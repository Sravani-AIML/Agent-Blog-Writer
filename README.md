# 🤖 Agentic Blog Writer
 
> An autonomous multi-agent AI pipeline that researches, writes, and publishes fully grounded 2,000+ word blog posts with citations, code snippets, and AI-generated images — in under 3 minutes.
 
[![Live Demo - Deployed on AWS](https://img.shields.io/badge/🚀_Live_Demo-Click_Here-blue?style=for-the-badge)](http://blog-writer-env.eba-3dpcebgm.us-east-1.elasticbeanstalk.com)

## 📸 Demo
 
[![Watch Demo Video](https://img.shields.io/badge/▶_Watch_Demo-OneDrive-blue?style=for-the-badge)](https://1drv.ms/v/c/ad2361dadd0a95e7/IQDZHVOg6dEWQ4HVGaOkIPkYAeMT3h-pJGj2tKyt0Gkd5Xw?e=REyVNN)
 
> *Real-time agent node execution visible in the Streamlit interface — watch the pipeline run live!*
 
---
 
## ✨ Features
 
- **Fully autonomous** — just enter a topic and the agents do the rest
- **Grounded content** — every claim backed by real-time web research via Tavily (6 parallel queries)
- **AI-generated images** — a 3-node Gemini image subgraph automatically places up to 3 contextual diagrams per article
- **2,000+ word output** — structured blog posts with citations, code snippets, and source URLs
- **Under 3 minutes** — from topic input to fully formatted blog post
- **98% faster** than manual blog writing
- **Real-time UI** — multi-tab Streamlit interface showing live node execution, Evidence, Markdown Preview, Images, and Logs
- **Production deployed** — live on AWS Elastic Beanstalk via Docker
---
 
## 🏗️ Architecture
 
The system is composed of two LangGraph pipelines that run together to produce a fully grounded, image-enriched blog post.
 
| 🔷 Main Pipeline | 🖼️ Image Subgraph |
|:---:|:---:|
| <img width="160" height="630" alt="Main Pipeline" src="https://github.com/user-attachments/assets/902cee81-7a5c-465e-82a2-60319e323126" /> | <img width="252" height="432" alt="Image Subgraph" src="https://github.com/user-attachments/assets/a228b637-032f-48ad-ae2d-5c096c6e6e4a" /> |
 
> The dashed conditional edges mean the **router** can loop back to **research**, and the **orchestrator** can loop back to **worker** — enabling iterative refinement before producing the final output. The Image Subgraph runs in parallel with the main pipeline.

### Node Responsibilities
 
| Pipeline | Node | Role |
|----------|------|------|
| Main | **router** | Classifies the topic and decides whether more research is needed (can loop) |
| Main | **research** | Runs 6 parallel Tavily queries to gather real-time evidence and source URLs |
| Main | **orchestrator** | Plans blog structure and assigns sections to workers (can loop for quality) |
| Main | **worker** | Writes individual sections grounded in research context |
| Main | **reducer** | Merges all worker sections into a cohesive 2,000+ word article with citations |
| Image | **merge_content** | Combines blog content and research context for image planning |
| Image | **decide_images** | Determines where and what type of images best fit the content |
| Image | **generate_and_place_images** | Generates up to 3 Gemini images and places them inline in the blog |
 
---
 
## 🛠️ Tech Stack
 
| Category | Tools |
|----------|-------|
| **Agent Framework** | LangGraph, LangChain |
| **LLMs** | GPT-4o (writing), Gemini (image generation) |
| **Web Research** | Tavily Search API |
| **Frontend** | Streamlit (multi-tab, real-time streaming) |
| **Containerization** | Docker |
| **Cloud Deployment** | AWS Elastic Beanstalk |
| **Language** | Python 3.11 |
 
---
 
## 🚀 How It Works
 
1. **Enter a topic** in the Streamlit UI (e.g. *"The Future of Agentic AI"*)
2. The **Router** classifies the topic and kicks off the pipeline
3. The **Research node** fires 6 Tavily queries in parallel, gathering real-time evidence, URLs, and key facts
4. The **Orchestrator** reads the research and plans a full blog structure — intro, sections, conclusion
5. **Parallel Workers** each write one section simultaneously, grounded in the research context
6. The **Reducer** merges all sections into a polished 2,000+ word article with citations and source URLs
7. Simultaneously, the **Image Subgraph** (merge → decide → generate) uses Gemini to auto-place up to 3 contextual diagrams
8. The final blog renders in the **Markdown Preview tab** — ready to publish
### Streamlit UI Tabs
 
| Tab | What You See |
|-----|-------------|
| **Live Execution** | Real-time node-by-node progress as the pipeline runs |
| **Evidence** | All research sources and retrieved web snippets |
| **Markdown Preview** | The fully formatted final blog post |
| **Images** | AI-generated contextual diagrams |
| **Logs** | Full pipeline execution logs |
 
---
 
## ⚙️ Local Setup
 
### Prerequisites
 
- Python 3.11+
- OpenAI API key
- Google Gemini API key
- Tavily API key
### Installation
 
```bash
# Clone the repo
git clone https://github.com/Sravani-AIML/Agent-Blog-Writer.git
cd Agent-Blog-Writer
 
# Install dependencies
pip install -r requirements.txt
```
 
### Environment Variables
 
Create a `.env` file in the root directory:
 
```env
OPENAI_API_KEY=your_openai_api_key
GOOGLE_API_KEY=your_gemini_api_key
TAVILY_API_KEY=your_tavily_api_key
```
 
### Run Locally
 
```bash
streamlit run app.py
```
 
Open your browser at `http://localhost:8501`
 
---
 
## 🐳 Docker
 
```bash
# Build the image
docker build -t agent-blog-writer .
 
# Run the container
docker run -p 8501:8501 \
  -e OPENAI_API_KEY=your_key \
  -e GOOGLE_API_KEY=your_key \
  -e TAVILY_API_KEY=your_key \
  agent-blog-writer
```
 
---
 
## ☁️ AWS Deployment
 
This app is deployed on **AWS Elastic Beanstalk** using Docker.
 
The `Dockerrun.aws.json` file configures the Elastic Beanstalk environment to pull and run the Docker container. Deployment steps:
 
```bash
# Initialize EB CLI
eb init -p docker agent-blog-writer
 
# Create environment
eb create blog-writer-env
 
# Deploy
eb deploy
```
 
---
 
## 📂 Project Structure
 
```
Agent-Blog-Writer/
├── app.py                  # Streamlit UI and entry point
├── bwa_writer.py           # LangGraph pipeline (all agent nodes)
├── requirements.txt        # Python dependencies
├── Dockerfile              # Docker build config
├── Dockerrun.aws.json      # AWS Elastic Beanstalk config
├── .dockerignore
├── .ebignore
├── images/                 # Screenshots and demo assets
└── *.md                    # Sample generated blog posts
```
 
---










