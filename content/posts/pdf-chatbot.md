---
date: '2025-05-02T01:45:43-07:00'
draft: false
title: 'Learning AI Engineering: My PDF Q&A Bot Journey'
---
I've been diving into AI engineering concepts and recently I've been working with an AI model from huggingface, and using LocalAI, qdrant, and python to develop a simple Q and A chatbot, that can return information from any pdf file! I got started by following Zen Van Riel's excellent course in the Skool community. If you're interested in learning AI engineering, I highly recommend checking out his community: [AI Engineer on Skool](https://www.skool.com/ai-engineer/about?ref=8b5f8176d7084f05b196670907dcd919).

## Key Components

The current implementation runs LocalAI and Qdrant in Docker containers, with models downloaded locally via a script I created called `download_models`. This setup forms the foundation of everything that makes the Q&A functionality work.

The PDF Q&A system consists of two main servers:

1. **Embeddings Server**: Transforms text chunks into vector representations that capture semantic meaning
2. **PDF Q&A Server**: Orchestrates the entire process, handling:
    - PDF uploads and text extraction
    - Communication with the embeddings service
    - Vector similarity search (via Qdrant)
    - Question processing
    - Streaming results back to the user

## Future Goals

While I'm happy with the current implementation, there's still more I want to do:

1. **Integrate Local Model with GPU acceleration**: Run AI models directly on my machine to leverage GPU acceleration rather than using containers.
2. **Cloud AI Integration**: Experiment with various cloud AI services to compare performance and capabilities.
3. **Home Lab Setup**: Configure my old gaming PC as a dedicated workspace for AI experimentation.

## Try It Yourself

You can find the complete code on GitHub: [eccentricnode/qa-chatbot](https://github.com/eccentricnode/qa-chatbot/)

If you're interested in AI engineering and building similar projects, I highly recommend checking out Zen Van Riel's course in the AI Engineer Skool community. It's been invaluable in helping me understand both the theoretical concepts and practical implementation details.

