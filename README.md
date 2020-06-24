# MRI_image_reconstruction

🚀 This project was created using the [ml-app-template](https://github.com/madewithml/ml-app-template) cookiecutter template. Check it out to start creating your own ML applications.

## Set up
```
virtualenv -p python3 venv
source venv/bin/activate
pip install -r requirements.txt
```

## Training
```bash
python mri_image_reconstruction/train.py
```
## Inference via scripts
```bash
python mri_image_reconstruction/predict.py
```

## Endpoints
```bash
uvicorn app:app --host 0.0.0.0 --port 5000 --reload
→ http://localhost:5000/docs
```

## Inference via API
```python
import json
import requests

headers = {
    'accept': 'application/json',
    'Content-Type': 'application/json',
}

data = '''{"experiment_id": "latest",
           "X": ""}'''

response = requests.post('http://0.0.0.0:5000/predict',
                         headers=headers, data=data)
results = json.loads(response.text)
print (json.dumps(results, indent=2, sort_keys=False))
```

## TensorBoard
```bash
tensorboard --logdir tensorboard
→ http://localhost:6006/
```

## Tests
```bash
pytest
```

## Docker
1. Build image
```bash
docker build -t mri-image-reconstruction:latest -f Dockerfile .
```
2. Run container
```bash
docker run -d -p 5000:5000 -p 6006:6006 --name mri-image-reconstruction mri-image-reconstruction:latest
```

## Directory structure
```
mri-image-reconstruction/
├── datasets/                           - datasets
├── experiments/                        - experiment directories
├── logs/                               - directory of log files
|   ├── errors/                           - error log
|   └── info/                             - info log
├── tensorboard/                        - tensorboard logs
├── tests/                              - unit tests
├── mri_image_reconstruction/    - ml scripts
|   ├── app.py                            - app endpoints
|   ├── config.py                         - configuration
|   ├── data.py                           - data processing
|   ├── models.py                         - model architectures
|   ├── predict.py                        - inference script
|   ├── train.py                          - training script
|   └── utils.py                          - load embeddings
├── .dockerignore                       - files to ignore on docker
├── .gitignore                          - files to ignore on git
├── CODE_OF_CONDUCT.md                  - code of conduct
├── CODEOWNERS                          - code owner assignments
├── config.py                           - configuration
├── CONTRIBUTING.md                     - contributing guidelines
├── Dockerfile                          - dockerfile to containerize app
├── LICENSE                             - license description
├── logging.json                        - logger configuration
├── README.md                           - this README
└── requirements.txt                    - requirements
```

## Overfit to small subset
```
python mri-image-reconstruction/train.py --overfit
```

## Experiments
```
```

## Helpful docker commands
• Build image
```
docker build -t mri-image-reconstruction:latest -f Dockerfile .
```

• Run container if using `CMD ["python", "app.py"]` or `ENTRYPOINT [ "/bin/sh", "entrypoint.sh"]`
```
docker run -p 5000:5000 --name mri-image-reconstruction mri-image-reconstruction:latest
```

• Get inside container if using `CMD ["/bin/bash"]`
```
docker run -p 5000:5000 -it mri-image-reconstruction /bin/bash
```

• Other flags
```
-d: detached
-ti: interative terminal
```

• Clean up
```
docker stop $(docker ps -a -q)     # stop all containers
docker rm $(docker ps -a -q)       # remove all containers
docker rmi $(docker images -a -q)  # remove all images
```