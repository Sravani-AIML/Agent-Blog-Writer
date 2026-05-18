# 🤖 Agentic Blog Writer
 
> An autonomous multi-agent AI pipeline that researches, writes, and publishes fully grounded 2,000+ word blog posts with citations, code snippets, and AI-generated images — in under 3 minutes.
 
[![Live Demo](https://img.shields.io/badge/🚀_Live_Demo-Click_Here-blue?style=for-the-badge)](http://blog-writer-env.eba-3dpcebgm.us-east-1.elasticbeanstalk.com)
[![GitHub](https://img.shields.io/badge/GitHub-Agent--Blog--Writer-black?style=for-the-badge&logo=github)](https://github.com/Sravani-AIML/Agent-Blog-Writer)
[![Python](https://img.shields.io/badge/Python-3.11-blue?style=for-the-badge&logo=python)](https://python.org)
[![Deployed on AWS](https://img.shields.io/badge/AWS-Elastic_Beanstalk-orange?style=for-the-badge&logo=amazonaws)](https://aws.amazon.com/elasticbeanstalk/)
# 🤖 Agentic Blog Writer

An autonomous multi-agent AI pipeline that researches, writes, and publishes fully grounded 2,000+ word blog posts with citations, code snippets, and AI-generated images — in under 3 minutes.
http://blog-writer-env.eba-3dpcebgm.us-east-1.elasticbeanstalk.com
## 📸 Demo

https://1drv.ms/v/c/ad2361dadd0a95e7/IQDZHVOg6dEWQ4HVGaOkIPkYAeMT3h-pJGj2tKyt0Gkd5Xw?e=REyVNN

Real-time agent node execution visible in the Streamlit interface — watch the pipeline run live!

✨ Features

- Fully autonomous — just enter a topic and the agents do the rest
- Grounded content — every claim backed by real-time web research via Tavily (6 parallel queries)
- AI-generated images — a 3-node Gemini image subgraph automatically places up to 3 contextual diagrams per article 2,000+ word output — structured blog posts with citations, code snippets, and source URLs
- Under 3 minutes — from topic input to fully formatted blog post
- 98% faster than manual blog writing
- Real-time UI — multi-tab Streamlit interface showing live node execution, Evidence, Markdown Preview, Images, and Logs
- Production deployed — live on AWS Elastic Beanstalk via Docker

# 🏗️ Architecture

The system is composed of two LangGraph pipelines that run together to produce a fully grounded, image-enriched blog post.
## 🔷 Main Pipeline

<img width="160" height="630" alt="image" src="https://github.com/user-attachments/assets/902cee81-7a5c-465e-82a2-60319e323126" />

The dashed conditional edges mean the router can loop back to research, and the orchestrator can loop back to worker — enabling iterative refinement before producing the final output.

# 🖼️ Image Subgraph

Runs in parallel with the main pipeline to generate and place contextual images:

<img width="252" height="432" alt="image" src="https://github.com/user-attachments/assets/a228b637-032f-48ad-ae2d-5c096c6e6e4a" />
Node Responsibilities
PipelineNodeRoleMainrouterClassifies the topic and decides whether more research is needed (can loop)MainresearchRuns 6 parallel Tavily queries to gather real-time evidence and source URLsMainorchestratorPlans blog structure and assigns sections to workers (can loop for quality)MainworkerWrites individual sections grounded in research contextMainreducerMerges all worker sections into a cohesive 2,000+ word article with citationsImagemerge_contentCombines blog content and research context for image planningImagedecide_imagesDetermines where and what type of images best fit the contentImagegenerate_and_place_imagesGenerates up to 3 Gemini images and places them inline in the blog

🛠️ Tech Stack
CategoryToolsAgent FrameworkLangGraph, LangChainLLMsGPT-4o (writing), Gemini (image generation)Web ResearchTavily Search APIFrontendStreamlit (multi-tab, real-time streaming)ContainerizationDockerCloud DeploymentAWS Elastic BeanstalkLanguagePython 3.11

🚀 How It Works

Enter a topic in the Streamlit UI (e.g. "The Future of Agentic AI")
The Router classifies the topic and kicks off the pipeline
The Research node fires 6 Tavily queries in parallel, gathering real-time evidence, URLs, and key facts
The Orchestrator reads the research and plans a full blog structure — intro, sections, conclusion
Parallel Workers each write one section simultaneously, grounded in the research context
The Reducer merges all sections into a polished 2,000+ word article with citations and source URLs
Simultaneously, the Image Subgraph (merge → decide → generate) uses Gemini to auto-place up to 3 contextual diagrams
The final blog renders in the Markdown Preview tab — ready to publish

Streamlit UI Tabs
TabWhat You SeeLive ExecutionReal-time node-by-node progress as the pipeline runsEvidenceAll research sources and retrieved web snippetsMarkdown PreviewThe fully formatted final blog postImagesAI-generated contextual diagramsLogsFull pipeline execution logs

⚙️ Local Setup
Prerequisites

Python 3.11+
OpenAI API key
Google Gemini API key
Tavily API key

Installation
bash# Clone the repo
git clone https://github.com/Sravani-AIML/Agent-Blog-Writer.git
cd Agent-Blog-Writer

# Install dependencies
pip install -r requirements.txt
Environment Variables
Create a .env file in the root directory:
envOPENAI_API_KEY=your_openai_api_key
GOOGLE_API_KEY=your_gemini_api_key
TAVILY_API_KEY=your_tavily_api_key
Run Locally
bashstreamlit run app.py
Open your browser at http://localhost:8501

🐳 Docker
bash# Build the image
docker build -t agent-blog-writer .

# Run the container
docker run -p 8501:8501 \
  -e OPENAI_API_KEY=your_key \
  -e GOOGLE_API_KEY=your_key \
  -e TAVILY_API_KEY=your_key \
  agent-blog-writer

☁️ AWS Deployment
This app is deployed on AWS Elastic Beanstalk using Docker.
The Dockerrun.aws.json file configures the Elastic Beanstalk environment to pull and run the Docker container. Deployment steps:
bash# Initialize EB CLI
eb init -p docker agent-blog-writer

# Create environment
eb create blog-writer-env

# Deploy
eb deploy

📂 Project Structure
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




