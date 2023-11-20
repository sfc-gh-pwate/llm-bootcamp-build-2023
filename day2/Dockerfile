FROM rapidsai/rapidsai:23.04-cuda11.8-runtime-ubuntu22.04-py3.8

RUN apt-get update && apt-get install -y --no-install-recommends

WORKDIR /notebooks
# Copy Notebooks and data into the container at /notebooks
COPY llm-day2-notebook.ipynb .
COPY llm-day2-notebook-fine-tuned-full-dataset.ipynb .
COPY utils.py .
COPY connection.json .
COPY data/transcripts.json .

RUN conda install -n rapids -c https://repo.anaconda.com/pkgs/snowflake snowflake-snowpark-python pandas jupyterlab

# Make port 8888 available to the world outside this container
EXPOSE 8888

# Run JupyterLab on port 8888 when the container launches
CMD ["/opt/conda/envs/rapids/bin/jupyter", "llm-finetune", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root", "--NotebookApp.token=''", "--NotebookApp.password=''"]
