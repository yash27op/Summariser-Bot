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
