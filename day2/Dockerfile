FROM rapidsai/rapidsai:23.04-cuda11.8-runtime-ubuntu22.04-py3.8

RUN apt-get update && apt-get install -y --no-install-recommends

WORKDIR /notebooks
COPY environment.yml /notebooks

RUN conda --version
RUN conda env create -f environment.yml

# Copy Notebook and data into the container at /app
COPY notebook.ipynb .
COPY connection.json .

# Make ports 8888 and 8080 available to the world outside this container
EXPOSE 8888

# Run JupyterLab on port 8888 when the container launches
CMD ["/opt/conda/envs/rapids/bin/jupyter", "lab", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root", "--NotebookApp.token=''", "--NotebookApp.password=''"]
