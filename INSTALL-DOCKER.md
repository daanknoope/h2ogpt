### Containerized Installation for Inference on Linux GPU Servers

1. Build the container image:

```bash
docker build -t h2o-llm .
```

2. Run the container (you can also use `finetune.py` and all of its parameters as shown above for training):

```bash
docker run --runtime=nvidia --shm-size=64g -p 7860:7860 -v ${HOME}/.cache:/root/.cache --rm h2o-llm -it generate.py \
    --load_8bit=True --base_model='togethercomputer/GPT-NeoXT-Chat-Base-20B' --lora_weights=my_finetuned_weights --prompt_type=human_bot
```

3. Open `https://localhost:7860` in the browser

### Docker Compose Setup & Inference

1. (optional) Change desired model and weights under `environment` in the `docker-compose.yml`

2. Build and run the container

```bash
docker-compose up -d --build
```

3. Open `https://localhost:7860` in the browser

4. See logs:

```bash
docker-compose logs -f
```

5. Clean everything up:

```bash
docker-compose down --volumes --rmi all
```

