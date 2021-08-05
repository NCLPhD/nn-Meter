# Quick Start

## nn-Meter Installation

To install the latest version of nn-Meter, you should install the package through source code. First git clone nn-Meter package to local,
```Bash
git clone git@github.com:microsoft/nn-Meter.git
cd nn-Meter
```
Then simply run the following pip install in an environment that has `python >= 3.6`. 
```Bash
pip install .
```
The stable version of wheel binary pacakge will be released soon.


## "Hello World" example on torch model
nn-Meter is an accurate inference latency predictor for DNN models on diverse edge devices. nn-Meter supports tensorflow pb-file, onnx file, torch model and nni IR model for latency prediction.

Here is an example script to predict latency for Resnet18 in torch. To run the example, package `torch`, `torchvision` and `onnx` are required. The well tested version is `torch==1.9.0`, `torchvision==0.10.0` and `onnx==1.9.0`.   

```python
from nn_meter import load_latency_predictor
import torchvision.models as models

def main(args):
    base_model = models.resnet18()
    base_predictor = 'cortexA76cpu_tflite21'

    # load a predictor (device_inferenceframework)
    predictor = load_latency_predictor(base_predictor) 

    # predict the latency based on the given model
    lat = predictor.predict(model=base_model, model_type='torch', input_shape=[1, 3, 32, 32])
    print(f'Latency for {base_predictor}: {lat}(s)')

if __name__ == '__main__':
    main(params)
```

For more detailed usage of nn-Meter, please refer to [this doc](usage.md).