# ds-computer-vision with PyTorch
Welcome to the GitHub repository for exploring the exciting field of computer vision using PyTorch on the MNIST fashion. My project aims to demonstrate the capabilities of these powerful deep learning frameworks by training and evaluating various models on this widely-used dataset. Additionally, I have integrated MLflow to monitor and track the performance of the models, providing an efficient pipeline for fine-tuning and optimizing the deep learning parameters. I hope you find this repository informative and useful in your own computer vision projects.

If you want to see TensorFlow in action use this link: [TensorFlow](https://github.com/andrey101010/ds-computer-vision-2)

## Environment 
Use the [requirements](requirements.txt) file in this repo to create a new environment. 

```BASH
pyenv local 3.10.10
python -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt
```

## MLFlow
MLFlow is a tool for tracking ML experiments. You can run it locally or remotely. It stores all the information about experiments in a database. And you can see the overview via the GUI or access it via APIs. Sending data to mlflow is done via APIs. And with mlflow you can also store models on S3 where you version them and tag them as production for serving them in production.

The file to run the pytorch script and monitor it with mlflow is in mlflow_folder.

```BASH
python mlflow_folder/classification.py
```

The MLFLOW URI should **not be stored on git**, you have two options, to save it locally in the `.mlflow_uri` file:

```BASH
echo http://127.0.0.1:5000/ > .mlflow_uri
```

This will create a local file where the uri is stored which will not be added on github (`.mlflow_uri` is in the `.gitignore` file). Alternatively you can export it as an environment variable with

```bash
export MLFLOW_URI=http://127.0.0.1:5000/
```

This links to your local mlflow, if you want to use a different one, then change the set uri.

The code in the [config.py](modeling/config.py) will try to read it locally and if the file doesn't exist will look in the env var.. IF that is not set the URI will be empty in your code.


### Creating an MLFlow experiment

You can do it via the GUI or via [command line](https://www.mlflow.org/docs/latest/tracking.html#managing-experiments-and-runs-with-the-tracking-service-api) if you use the local mlflow:

```bash
mlflow experiments create --experiment-name 0-template-ds-modeling
```

Check your local mlflow

```bash
mlflow ui
```

and open the link [http://127.0.0.1:5000](http://127.0.0.1:5000)

This will throw an error if the experiment already exists. **Save the experiment name in the [config file](mlflow_folder/config.py).**

In order to train the model and store test data in the data folder and the model in models run:

