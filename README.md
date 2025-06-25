# Code Summarization

AI based PR summarization and Code Summarization.

---

## Requisites:

- Python version >=3.11 and <3.13
- Ollama with `granite3.1-dense:8b` model installed. (Any model can be used here. Make sure that the name is mentioned in `src/config/settings.yaml`)
- URL for a Redis instance, local or hosted (update this in `src/.env` using `src/.env.copy` as template. May use the same URL for Redis and Celery)
- A GitHub bot secret and its ID (update in `src/.env`, same as above)
- Poetry installed in your python environment.

## Steps:

- Set up virtual environment and install dependencies using `poetry install` (may need to use `poetry env activate` and run the output to get inside the new virtual environment)
- If dependencies are set up correctly, run the Celery script with `src/scripts/start_celery.sh`
- If GitHub bot info is updated in `src/.env`, commands can be used in any pull request in the repository with the bot installed.
  - `/summary` : Create summary for the files changed in the pull request commits.
  - `/review` : Review code quality and security features for the files changed in the pull request commits.
- `src/start.sh` can also be run to get info about ongoing and completed tasks.

# Prerequisites 

# Pull Request Summarizer

Python API application to generate code reviews and summaries for changes made in pull requests.

<img width="859" alt="Screenshot 2025-06-25 at 10 19 05 PM" src="https://github.com/user-attachments/assets/38f71da9-182e-4bca-a3a8-4fd4b9409ae9" />

---

## Prerequisites:

- Python 3.11 or 3.12
- [Redis](https://redis.io/docs/latest/operate/oss_and_stack/install/archive/install-redis/), for MacOS:
  
```bash
brew install redis
```
- Poetry:
```bash
pip install poetry
```
- Ollama set up locally:
  - Install [ollama](https://ollama.com/)
  - Download `granite3.1-dense:8b` (this is the default model used here; to use any other model from ollama, see [here](https://github.ibm.com/ibmcloud/prSummarizer/blob/pr-summarization/README.md#how-to-use-other-llms))
    
```bash
ollama pull granite3.1-dense:8b
```
- A GitHub bot set up as follows:

  - With permissions to read and write repository contents and comments on pull requests and issues:
  
  <img width="611" alt="Screenshot 2025-06-25 at 10 20 08 PM" src="https://github.com/user-attachments/assets/656e5a7b-8970-4032-ac8e-f528731a0464" />

   - Subscribed to events for comments created in issues and pull requests:

  <img width="545" alt="Screenshot 2025-06-25 at 10 21 01 PM" src="https://github.com/user-attachments/assets/2d9ed019-f43a-4fe1-b7c8-17bb89dc7b0f" />

  - Install the GitHub bot to the required repository.

## Installation:
- Optional; To create and use virtual environment:
```bash
poetry env use 3.11  # or 3.12, depending on your version of python
poetry env activate
```
  - This will output a command to activate the newly created virtual environment as follows:
```bash
source /path/to/project/.venv/bin/activate
```
  - Run this command to activate the virtual environment.
- To install dependencies, use `poetry`. In the project root folder, run:
```bash
poetry install --no-root
```
- Use the GitHub bot credentials (App ID and Secret Key) in `src/.env`.
- Have an instance of [webhook receiver](https://github.com/aamadeuss/webhook-receiver) running with the GitHub bot credentials.

## Steps:

- Once dependencies are set up correctly, run the Celery script with `src/scripts/start_celery.sh`
- If webhook receiver is up and running, the following commands can be used:
  - `/summary` : Create summary of all the changes made in the pull request commits.
  - `/review` : Review code quality and security features for the files changed in the pull request commits.
  
  
## How to use other LLMs:

- Install the model using ollama:
```bash
ollama pull <your-model>
```
- Edit `src/config/settings.yaml` with the ollama tag of your model:
```bash
MODEL: <your-model>
```
