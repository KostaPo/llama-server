FROM python:3.13-slim

RUN apt-get update && apt-get install -y git && rm -rf /var/lib/apt/lists/*

WORKDIR /app

RUN git clone https://github.com/ivanfioravanti/llm_context_benchmarks.git .

RUN pip install --no-cache-dir \
    openai \
    psutil \
    matplotlib \
    numpy \
    tiktoken \
    requests

# 0.5k убрали — скрипт принимает только целые числа
RUN python generate_context_files.py pride_and_prejudice.txt --sizes 1,2,4,8,16,32,64,128

RUN mkdir -p /results
VOLUME ["/results"]

ENTRYPOINT ["python", "benchmark.py"]