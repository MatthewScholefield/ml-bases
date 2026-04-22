# ML Base Images

Container base images for ML workloads, built on [Chainguard Wolfi](https://edu.chainguard.dev/).

## TensorFlow

Includes Python 3.12, [uv](https://docs.astral.sh/uv/), and a virtual environment at `/opt/venv` with TensorFlow (CUDA) pre-installed.

### Usage

```bash
docker run -it --rm --gpus all <username>/ml-tensorflow python -c "import tensorflow as tf; print(tf.config.list_physical_devices('GPU'))"
```

### Extending with additional packages

Create a Dockerfile based on this image:

```dockerfile
FROM <username>/ml-tensorflow

RUN uv pip install pandas scikit-learn matplotlib
```

Or install ad-hoc:

```bash
docker run -it --rm <username>/ml-tensorflow uv pip install pandas
```

The virtual environment is at `/opt/venv` and is activated by default via `PATH` and `VIRTUAL_ENV`.
