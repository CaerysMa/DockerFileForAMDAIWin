# Start from Ubuntu 22.04
FROM wsl_2_rocm_custom AS base

# Use ollama/ollama:rocm as a source for Ollama files
FROM ollama/ollama:rocm AS ollama_source

# Final stage
FROM base

# Set the working directory
WORKDIR /

# Install necessary packages
RUN apt-get update && \
    apt-get install -y ca-certificates && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Copy Ollama binary
COPY --from=ollama_source /usr/bin/ollama /usr/bin/ollama

# Copy Ollama libraries
COPY --from=ollama_source /usr/lib/ollama /usr/lib/ollama

# Expose the Ollama port
EXPOSE 11434

# Set the Ollama host
ENV OLLAMA_HOST=0.0.0.0

# Set the PATH
ENV PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# Set the entrypoint
ENTRYPOINT ["/usr/bin/ollama"]

# Set the default command
CMD ["serve"]
