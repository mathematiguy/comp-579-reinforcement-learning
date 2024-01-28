# This Makefile automates routine tasks for this Singularity-based project.
REPO_NAME := $(shell basename `git rev-parse --show-toplevel` | tr '[:upper:]' '[:lower:]')
IMAGE := container.sif
RUN ?= singularity exec $(FLAGS) $(IMAGE)
SINGULARITY_ARGS ?=
DVC_CACHE_DIR ?= $(shell dvc cache dir)
FLAGS ?=
VENV_PATH ?= venv

.PHONY: jupyter container shell

jupyter:
	$(RUN)  jupyter lab \
		--ip=0.0.0.0 \
		--no-browser \
		--port 8888

# Builds a Singularity container from the Singularity definition file.
# Note: This command requires sudo privileges.
container: $(IMAGE)
$(IMAGE): Singularity
	sudo singularity build $(IMAGE) $(SINGULARITY_ARGS) Singularity

# Starts a shell within the Singularity container, with the virtual environment activated.
shell:
	singularity shell $(FLAGS) $(IMAGE) $(SINGULARITY_ARGS) bash
