---
date: '2025-05-01T15:49:53-07:00'
draft: false
title: 'Adventures With AI, Docker, and running it on WSL 2'
---
# The WSL2 GPU Adventure: What I Learned While Trying to Accelerate an LLM

So I went on this adventure trying to get GPU acceleration working with my local AI model. I thought it would be straightforward – install some drivers, update a config file, and boom: speed boost. But like most things in tech, reality had other plans.

## The Setup

I started with a pretty solid machine:

- AMD Ryzen 7 CPU (with integrated graphics)
- NVIDIA RTX 3070 Ti GPU
- Windows 11 with WSL2 running Debian
- LocalAI and Qdrant in Docker containers

The CPU-only version was already working fine. The model responded to queries, the vector database stored embeddings properly – everything functioned. Just... slower than I wanted.

## The Problems

Getting GPU acceleration working in WSL2 turned into a rabbit hole of issues:

1. **The Dual GPU Problem** - My machine has both integrated Ryzen graphics AND the NVIDIA card. WSL2 seems genuinely confused by this setup.
2. **Docker Configuration** - The docker-compose.yml needed specific GPU configurations:
    
    yaml
    
    ```yaml
    runtime: nvidia
    environment:
      - NVIDIA_VISIBLE_DEVICES=all
      - NVIDIA_DISABLE_REQUIRE=1
    ```
    
3. **Driver Incompatibilities** - WSL2 access to NVIDIA GPUs requires precise combinations of Windows drivers, WSL kernel versions, and NVIDIA toolkit packages.
4. **Error Messages** - The most common one being: `nvidia-container-cli: requirement error: invalid expression: unknown`

## What Actually Worked

After hours of tweaking, reinstalling, and hair-pulling, I found a partial solution:

1. Adding `NVIDIA_DISABLE_REQUIRE=1` to the environment variables in docker-compose.yml
2. Using the simpler `runtime: nvidia` approach instead of the newer deploy/resources specification
3. Updating the model's YAML config to use GPU layers:
    
    yaml
    
    ```yaml
    gpu_layers: 35  # Changed from 0
    ```
    

But despite these changes, WSL2 still wouldn't fully utilize the GPU. It's like Windows and the Linux subsystem just couldn't agree on who gets to talk to the graphics card.

## Potential Alternative Path: Podman

During my research, I discovered Podman might offer a better approach for WSL2 GPU access. Unlike Docker, Podman:

- Uses a daemonless architecture (no background service)
- Employs Container Device Interface (CDI) for GPU access
- Offers better security through rootless containers
- Maintains Docker-compatible commands (easy transition)

This approach is backed by NVIDIA's own documentation, which recommends Podman as the preferred container engine for WSL2 with GPU access.

## Lessons Learned

1. **WSL2 Has Limits** - It's amazing technology, but GPU passthrough isn't fully mature yet, especially with dual-GPU setups.
2. **Container Architecture Matters** - The difference between Docker's daemon approach and Podman's daemonless design impacts GPU accessibility.
3. **Linux Is Still King for AI** - Native Linux installations offer significantly better GPU support for AI/ML workloads than Windows-based solutions.
4. **Persistence Pays Off** - Even though I didn't get full GPU acceleration, I learned a ton about containerization, WSL2 architecture, and NVIDIA's toolkit.

I'm still going to experiment with both running the model locally, without a wrapper like localai - after that I will likely test Podman next, and I'll test the same setup on my native Linux machine at home. For now, I'm using CPU-only mode with thread optimization to squeeze out reasonable performance.