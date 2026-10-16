# ml-space-benchmark-ky135

An unofficial Python distribution of
[SPACE at eec58a24516bfcd4554807b0a2b9d08b04eafd1c](https://github.com/apple-aiml-research/ml-space-benchmark/tree/eec58a24516bfcd4554807b0a2b9d08b04eafd1c).
The upstream Python source is unchanged. The distribution name distinguishes
this package from an official release by the SPACE authors.

## Build and use

```sh
uv build
uv venv --python 3.12
uv pip install --python .venv/bin/python dist/ml_space_benchmark_ky135-0.1.0-py3-none-any.whl
.venv/bin/python -I -m space.evaluate_qas --help
```

The import name remains `space`. Dataset files are not included. See the
upstream [README](https://github.com/apple-aiml-research/ml-space-benchmark/blob/eec58a24516bfcd4554807b0a2b9d08b04eafd1c/README.md) for dataset acquisition and benchmark commands.
The original source and attribution remain intact in the source distribution;
[LICENSE](https://github.com/apple-aiml-research/ml-space-benchmark/blob/eec58a24516bfcd4554807b0a2b9d08b04eafd1c/LICENSE), [LICENSE_DATA](https://github.com/apple-aiml-research/ml-space-benchmark/blob/eec58a24516bfcd4554807b0a2b9d08b04eafd1c/LICENSE_DATA), and
[ACKNOWLEDGEMENTS.md](https://github.com/apple-aiml-research/ml-space-benchmark/blob/eec58a24516bfcd4554807b0a2b9d08b04eafd1c/ACKNOWLEDGEMENTS.md) are also included in the wheel.

## Dependencies

Dependency bounds use the working dimOS integration as a conservative baseline;
this does not establish compatibility with every version in each range.
Upstream imports both API clients, image utilities, and navigation registrations
eagerly, so those dependencies are required even for text QA. The QA evaluator
also imports PyTorch through its vLLM helper. `opencv-contrib-python` supplies
`cv2` and avoids installing competing OpenCV distributions alongside dimOS.

Video tasks need an imageio video backend. Install it in the same environment:

```sh
uv pip install --python .venv/bin/python "imageio[ffmpeg]>=2.37,<3"
```

Text-only QA and scoring do not need this extra.

This package does not install a vLLM server. The upstream local-model backend
requires separate setup and is not validated here. API-based QA and scoring
do not require it.
Egocentric navigation still needs the separate Habitat-Sim 0.3.0 Conda setup
in the upstream README; no Habitat simulation is validated here.
