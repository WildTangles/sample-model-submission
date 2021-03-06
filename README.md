
# Brain-score sample model submission
This is the template module, to add your model implementation and submit it to brain-score. 
It provides examples and template methods for an easy submission.

## Getting started
To submit a model to brain-score, the source code has to be submitted as a zip file. The framework will unpack and 
install the code and its dependencies in a sandboxed environment and execute the brain-score benchmarks on it.
One submission can contain multiple models. Once all models are scored on the benchmarks, an email with the results 
is sent to the submitter. The results will *NOT* be made public without explicit approval of the repository owner.
Additionally the submitted content will not be accessible to any other than the automated benchmark framework, 
no human will see the implementations without consent.

### Setup
There are two options to set up the submission: Either clone this repository and add a model implementation here, 
or add the required submission modules to an existing repository.

#### Setup this repository
The submission can contain multiple models. To create a submission do following steps:
  1. Clone this repository and rename it.
  2. Install the repositories dependencies by executing `pip install .` in the projects root directory 
     (maybe also in a virtual environment)
  3. Add model implementations to the corresponding file(`models/base_model.py` or `models/brain_model.py`). 
     The methods are well commented and describe what to add and return. There are some example base model 
     implementations provided for common machine learning libraries in the examples folder.
  4. Add *ALL* required libraries to the setup.py. If dependencies are missing, the scoring mechanism will fail.
  5. Run a test run, to see if the scoring mechanism works, by executing the main method in the template module. 
     It will run a mock run of the benchmark process. The test takes a while since it attempts to find the right layers 
     on public data to commit to brain regions.

#### Add modules to existing project
As a second way you can add the required modules to an existing project. 
To do so, copy the packages `models` and `test` to the existing project. 
Make sure to add all the dependencies listed in setup.py to the other project. 
You can check if your submission is correct by executing the main method of the modules in `models` directory.

### What kind of model do I submit?
Brain-Score accepts two kinds of models. 
The first type are base models: standard neural networks that can produce activations in response to stimuli, 
but do not make any commitments to brain regions by themselves.
The other alternative are "brain models", which take a set of stimuli as input and produce brain-region-localized 
neural firing rates per stimuli.

If you choose to submit a base model, standard mapping procedures wil be applied 
to convert the base model into a brain model. 
This entails mapping model layers to brain regions, pixels to degrees visual angle, etc.

Depending on your choice you can implement either the `base_model.py` or `brain_model.py` module. 
If you're not sure what to choose, then the base model is most likely the right choice.

### Base models
We provide several base model implementations in the examples folder. 
The examples work with wrapper classes imported from [model-tools](https://github.com/brain-score/model-tools). 
There are more wrapper implementations avaiable in the 
[model-tools/activations](https://github.com/brain-score/model-tools/tree/master/model_tools/activations) package. 
For more details on how the benchmarking works, see this 
[jupyter notebook](https://github.com/brain-score/candidate_models/blob/master/examples/score-model.ipynb).
It is located in a repository, containing previously submitted model implementations. 
This is also a good project to see further examples.

### Brain models
To implement a brain model, the instance has to implement the 
[BrainModel interface](https://github.com/brain-score/brain-score/blob/master/brainscore/model_interface.py). 
An example of how to do that can be seen in this 
[jupyter notebook](https://github.com/brain-score/brain-score/blob/master/examples/benchmarks.ipynb).


### Create zip and submit   
Once you're confident that your implementation works and the test run returns successfully, 
you can submit the project by creating a zip file. 
The file has to contain the projects root directory as a single entry.
Go to the [brain-score](http://www.brain-score.org/) website, register and submit your model. 
Once the results are calculated, you will get an email. 
Attention: Depending on how many models you have specified in one submission, the process will take a while. 
Please do not submit more than 3 models at a time!

### Further documentation sources
The Brain-Score projects are open source and can be freely explored.

Important projects to have a look at could be:
 - The [brain-score](https://github.com/brain-score/brain-score) project itself, 
   which contains the benchmarking code plus a small set of locally executable benchmarks.
 - The [candidate_models](https://github.com/brain-score/model-tools) project contains standard reference 
   model implementations. This is a good project to explore how the model integration is done. 
 - The [model-tools](https://github.com/brain-score/candidate_models) project contains useful helper methods for adding 
   new base models and provides the standard tools to convert them into brain models.
