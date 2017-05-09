# Prairie ML Azure Workshop Instructions

In this workshop, you will design, implement and deploy a predicitive classification solution using Azure Machine Learning Studio and R (or python). We will be looking at predicting which formation a sample of natural gas came from based exclusively on the chemical composition of the gas samples (location information also is available, but where's the fun in that?). 

In the first part of the workshop, you will learn how to load a data set into the cloud and perform data cleaning and transformations from a simple web interface. You will be able to choose between a drag-and-drop set of modules or writing your own scripts.

Next, you will be experimenting with different classification algorithms and evaluating their relative efficacy. You will be evaluating models using concepts such as confusion matricies, precision and recall. 

Once you have decided on the type of algorithm to employ and your preprocessing data cleaning steps, you will deploy a live API to interact with your trained model.

This is a workshop, but it is not a "connect the dots" workshop. I will only give general guidelines and help using the graphical interface. I recommend you get into groups of 2-3 and work through together, discussing along the way. If you get stuck, ask a neighbour first and then me.

Those who finish early will have the opportunity to iterate and refine their model or create a client module to utilize their model.

## Data Prep

1. You can find the datasets on [this public dropbox folder](https://www.dropbox.com/sh/jf0w63jxhdvwqym/AACBKC4tDGqSuYo7KXiRmukca?dl=0_).
    * There is a raw and a clean dataset available. If you are pressed for time or are having problems, feel free to take the clean data set and jump ahead.
2. Log in to Azure Machine Learning Studio using your azure account or a guest login (if you don't want to create an azure account)
3. Upload your starter data sets. At the bottom left hand corner of the workspaces, there is a "+New" button. You can select to upload a data set from your local disk.
4. You can inspect the data set using built in visualization tools showing histograms or box/whisker plots. Get a feel for the data and identify things like missing data, incorrect units, and unnecessary features
5. Get to work cleaning the data! You can explore the different modules such as filtering columns, adding rows, etc.
    * Alternatively, if you're a savvy R/python dev then you may feel more at home just busting it out in code. As you prefer.
6. I strongly recommend that you filter the data set to only records containing ~100 examples for a given formation. Otherwise, the models turn out to be pretty lackluster.

## Training the models

1. Split your data sets into training and test data. There is a drag'n'drop module for this.
2. You can select a model from the "Initialize Model" category under the "Machine Learning" group. 
3. To train a model, you drop a "Train Model" module onto the work canvas and connect your algorithm and training data nodes to it.
4. You can then drop a "Score Model" module onto the canvas and connect your trained model and test data nodes to it
5. The "Evaluate model" module is used to evaluate the results of training. You can evaluate two models side by side.
6. Train, score, and evaluate several classification algorithms. Try and choose the best one. 
    * Keep in mind pure "accuracy" can be deceiving

## Create the predictive service

1. Once you have selected your model of choice, you can select the trained model (make sure it's highlighted!), navigate to the control panel at the bottom of page, and click "Set up Web Service"
2. Enjoy the animation as the studio does the majority of work for you
3. There will most likely be some changes you need to make at this point. There are two paths displayed: the path of the training data set, and the path of new input data from the web service.
    + Not all the same processing steps need to be performed on the input data, which you can expect to be clean
    + You will have to connect the web module node to the proper place in your process. If you connect it above a module that, say, drops several columns, then your API will actually expect that the user populates those columns (even though they will be dropped)
    + In case it's not perfectly clear, you want to run the minimum necessary steps on the web service input.
4. Run the experiment to make sure everything resolves properly

## Deploy the web service

1. If your model ran properly, you can now click "Deploy Web Service." If presented with the option, choose the new version.
2. The application should bring you to your newly created web service! Test it out with the swagger api in the browser.

## For the extra achievers

- Try and see if you can improve your chosen model's performance. The azure ML studio offers several hyper parameters which can be manipulated for each model.
- See if you can create new features, eliminate unnecessary features, or manipulate the data in order to generate a better scoring model
- Try creating a client in your favourite programming language to consume your new API
- If you do all of that in two hours and still need more, then try find someone who needs help. If no one needs help and I made this too easy, start drafting up a scathing review for the meetup group. 
