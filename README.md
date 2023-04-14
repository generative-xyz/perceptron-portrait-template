# Become the next Perceptron artist

This template provide necessary tool to load a Perceptron model (including its lifecycle) from token seed, and classify images using the model.

This template is based on the [simple Bitcoin generative art template](https://github.com/generative-xyz/generative-xyz-template-simple).

## API

### getModelFromURI

```
async getModelFromURI(uri: string): Model
```

**Description:** Fetch model description from an URI endpoint, and load the model from description

**Parameters:**
- `uri: string` - The URI of the JSON file describing the model

**Return:** The loaded model, which is an instance of the Model class


### Model.classifyImage

```
classifyImage(pixels: number[]): number[]
```

**Description:** Classify the input image

**Parameters:**
- `pixel: number[]` - 1D array of size `w * h * c`, each number from `0` to `255` describing the pixels value of the image (`w`, `h`, `c` are the input dimension of the model, see for more detail)

**Return:** An array of number from `0` to `1`, describing for each class the probability of this image belonging to that class


### Model.getInfo

```
getInfo(): {
    modelName: string,
    classesName: string[],
    inputDim: number[3],
    hiddenNeurons: number[],
    activationFunc: string,
    parameters: {w: Tensor, b: Tensor}[],
}
```

**Description:** Return the information of the model

**Parameters:** None

**Return:** An object containing the information of the model
- `modelName` - A `string` describes model's name
- `classesName` - Array of `string` describes the name of image classes that the model will classify
- `inputDim` - Array of three `number` describes the three dimensions (width, height, number of channels) of the input images
- `hiddenNeurons` - Array of `number` describes the number of neurons in each hidden layer
- `activationFunc` - A `string` describes the name of the activation function (`ReLU`, `LeakyReLU`, `Tanh` or `Sigmoid`) used in each hidden layer
- `parameters` - An array containing the parameters of the model. Each element describe the weight (`w`) and bias (`b`) matrices of a hidden layer. 

### Tensor

Represent a 2D matrix. Contain the following attributes:
- `n`: number of rows in the matrix
- `m`: number of columns in the matrix
- `mat`: An 2D array which is the content of the matrix
  






The template support loading model from:
- JSON URI of a perceptron model 
- Inscription URI of a Perceptron collection item
- Token Seed (from 1 to 580) of a Perceptron collection item

This template is based on the [simple Bitcoin generative art template](https://github.com/generative-xyz/generative-xyz-template-simple).
