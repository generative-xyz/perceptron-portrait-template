# Become the next Perceptron artist

This template provide necessary tool to load a Perceptron model (including its lifecycle) from token seed, and classify images using the model.

This template is based on the [simple Bitcoin generative art template](https://github.com/generative-xyz/generative-xyz-template-simple).

## API

### getBrain

```
async getBrain(perceptronSeed: number, customModelEndpoint: string): Brain
```

**Description:** Fetch the Perceptron (along with its default model) from the specified token seed. If `customModelEndpoint` is specified, the loaded Perceptron will use the model at `customModelEndpoint` instead.

**Parameters:**
- `perceptronSeed: number` - From `1` to `580`, specify the token seed of the Perceptron
- `customModelEndpoint: string` - The URI of the JSON file describing the custom model the Perceptron will use

**Return:** The loaded Perceptron, which is an instance of the `Brain` class


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
    generalInfo: {
        modelName: string,
        classesName: string[],
        inputDim: number[3],
        totalNeurons: number[],
        activationFunc: string,
        parameters: {w: Tensor, b: Tensor}[],
    },
    lifeCycleInfo: {
        stage: number,
        stageRatio: number,
        age: number,
        growth: number,
        neuronsLife: number[][],
        nextStateTimestamp: number,
        nextStableTimestamp: number,
        rebirthCount: number,
    }
}
```

**Description:** Return the information of the model

**Parameters:** None

**Return:** An object containing the information of the model
- `generalInfo`
    - `modelName` - A `string` describes model's name
    - `classesName` - Array of `string` describes the name of image classes that the model will classify
    - `inputDim` - Array of three `number` describes the three dimensions (width, height, number of channels) of the input images
    - `hiddenNeurons` - Array of `number` describes the number of neurons in each hidden layer
    - `activationFunc` - A `string` describes the name of the activation function (`ReLU`, `LeakyReLU`, `Tanh` or `Sigmoid`) used in each hidden layer
    - `parameters` - An array containing the parameters of the model. Each element describe the weight (`w`) and bias (`b`) matrices of a hidden layer. 
- `lifeCycleInfo`
    - `stage` - A number from `1` to `5` describe the current state of the model (`1`: Growing, `2`: Stable, `3`: Decaying, `4`: Dead, `5`: Rebirth)
    - `stageRatio` - A number from `0` to `1` describe the elapsed portion of current state
    - `age` - A number from `0` to `60` describe the current age of the model in Perceptron Year
    - `growth` - A number from `0` to `1` describe the current activation of the Perceptron
    - `neuronsLife` - A 2D arrays of number from `0` to `1` describing the activation level of each neurons in the Perceptron
    - `nextStateTimestamp` - The timestamp of the next moment that the Perceptron will change its state
    - `nextStableTimestamp` - The timestamp of the next moment that the Perceptron will enter the Stable state
    - `rebirthCount` - A number describe the number of rebirth the Perceptron has went through

### Tensor

Represent a 2D matrix. Contain the following attributes:
- `n`: number of rows in the matrix
- `m`: number of columns in the matrix
- `mat`: An 2D array which is the content of the matrix
  