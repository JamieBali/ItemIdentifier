# Fuzzy Object Recommendation through Neural Construction

Object recommendation exists in a very refined structure. You can input a selection of parameters and a hard coded system will give you a list of recommendations. This is the way that websites like Amazon are able to recommend a good product based on your input.
 
The primary downside of a system like this is its exploitability. If we want our product to reach the top page of Amazon, we just need to give it a name containing every single keyword and give it hundreds of tags.

We don't here intend to rewrite the way these systems work, but rather introduce a new system for object recommendation based on neural keyword selection.

## The System

Our system is very similar to a simple keyword pull like Amazon provides, but with the added step of neural adaptation.

The system will be given a selection of labeled data which describes the objects. For each of the objects, we create a neural representation using keywords pulled from the keywords in the descriptor. We pick the top-k distinct (NLTK SemSim < 0.5) words from the full corpus to act as our object attributes.

With our neural representation of the object created, we are able to start taking in training input. Each time data comes through, we can use hebbian learning to enforce accuracy and lower the bonds of innacuracies.

### Training

The training will be fairly standard. We will obtain a full corpus of descriptions of every object. Optimally, these descriptions will contain explanations of what the objects look like, their function, their use, and any other important descriptions a client may need - this will of course be generated dynamically. We expect accuracy to be higher if all objects use the same convention for description (i.e. if you use physical description and function to describe one object, you should only use those characteristics to describe other objects - no more, no less)

The training process will contain a full corpus counter, which will count every keyword (ignoring stopwords) to figure out the top-k words in the corpus to act as a basis for our neural attributes. An additional check will make sure all of these k words are distinct (i.e. we don't want fast and quick to both be keywords).

Next, we find a full similarity between the descriptor for each object and the top-k words.

### Full Similarity

The full similarity measure needs to be the same in both the training and running of the system. It will, on a basic level, look through a descriptor and perform a semantic similarity between every word in the descriptor, and ever one of the top-k words generated in training, generating a value for every one of the top-k words. This neural representation can be displayed in a radar graph.

We can, and should, add an additional check that looks through context to see if the descriptor contains an inverter, like the word "not", and then use the inverse of the similarity.

### Use and Hebbian Learning

The network can be used by finding the full similarity of an input paragraph, and then comparing the resultant neural map to all other neural maps we've generated. The one with the highest similarity is the recommended object.

We can ask the user to input the accuracy of the system with a simple y/n question, or by giving them a list of the top-x objects and having them pick which one is the best for them

