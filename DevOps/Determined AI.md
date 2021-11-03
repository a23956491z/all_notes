create virtual env
```bash
# Start a Determined cluster locally.
python3.7 -m venv ~/.virtualenvs/test
. ~/.virtualenvs/test/bin/activate
pip install determined

```

install docker &  [nvidia-container-toolkit](https://aur.archlinux.org/packages/nvidia-container-toolkit/)
deploy
```bash
# To start a cluster with GPUs, remove `no-gpu` flag.
det deploy local cluster-up --no-gpu
# Access web UI at localhost:8080. By default, "determined" user accepts a blank password.

# Navigate to a Determined example.
git clone https://github.com/determined-ai/determined
cd determined/examples/computer_vision/cifar10_pytorch

# Submit job to train a single model on a single node.
det experiment create const.yaml .
```