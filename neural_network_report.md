<h1>Neural Network Report</h1>

<h3>OVERVIEW</h3>
The nonprofit foundation Alphabet Soup wants a tool that can help it select applicants for funding with the best chance of success in their ventures.  Aplphabet Soup's business team provided a CSV containing more than 34,000 organizations that have received funding from Alphabet Soup over the years. Within this dataset are columns that capture metadata about each organization and whether the venture was considered successful or not.

Modeling was done with a neural network to predict successful ventures.  A target accuracy of 75% or better was desired, which was not achieved during this work after many optimization attempts.  Accuracy for the produced models was never better than just above 73%.

<h4>METHODS</h4>
<h6>DATA PREPROCESSING</h6>
The CSV contained 12 columns.  The column IS_SUCCESSFUL was the target variable.  Columns EIN and NAME were idenintification columns and were dropped from all models as not determinative of success or failure, leaving these features:<br>
- APPLICATION_TYPE — Alphabet Soup application type<br>
- AFFILIATION — Affiliated sector of industry<br>
- CLASSIFICATION — Government organization classification<br>
- USE_CASE — Use case for funding<br>
- ORGANIZATION — Organization type<br>
- STATUS — Active status<br>
- INCOME_AMT — Income classification<br>
- SPECIAL_CONSIDERATIONS — Special considerations for application<br>
- ASK_AMT — Funding amount requested<br>

<h6>OPTIMIZATION</h6>
Many attempts were made to optimize the model to achieve the desired 75% accuracy.  Three attemps are documented for reference and for further work, as versions 1, 2, and 3, or v1, v2, and v3.  All attempts used relu as the activation functions for the hidden layers, as tanh was found to perform slightly worse, and each model has a single output layer using sigmoid as the activation function.

In v1, application types with fewer than 500 entries were grouped into an Other category, as were classification types with fewer than 100 entries.  A neural network was built with two hidden layers of 10 and 4 nodes, respectively, and trained with 10 epochs.  Accuracy was about 72.7% at best.  Adding more nodes, layers, or epochs did not appreciably improve the performance, so some attempt was made to minimize these values to streamline the model, since higher accuracy was not attainable.

In v2, the column STATUS was also dropped from consideration, application types with fewer than 500 entries were grouped into an Other category, as were classification types with fewer than 100 entries.  A neural network was built with two hidden layers of 45 and 12 nodes, respectively, and trained with 15 epochs.  Performace was very slightly improved with an accuracy of 73.1% at its best, but with much more complexity in the neural network.

In v3, the columns STATUS and SPECIAL_CONSIDERATIONS were both dropped from consideration, application types with fewer than 1000 entries were grouped into an Other category, as were classification types with fewer than 1000 entries.  A neural network was built with four hidden layers of 100, 50, 10, and 4 nodes, respectively, and trained with 100 epochs.  The question in version 3 was if moving more items into the Other categories and grossly increasing the complexity of the model would produce better performance, but it did not.  In fact, accuracy on the test data dropped from 73.1% in v2 to 72.9% in v3, perhaps indicating overfitting (since the accuracy scores during evaluations of the epochs were slightly higher than in v2).

<h4>RESULTS</h4>
Version 2 ended up having the highest accuracy, but was only slightly better than the much simpler Version 1 model despite greatly increased complexity, and still fell short of the desired 75%.  If no further work were to be done, it would be recommended to use Version 1, as it produces nearly identical results with a much simpler model.  If further work were to be done, it would be recommended to use Version 1 as the baseline to continue with, as the limit on the accuracy did not seem to depend on increased neural network complexity.

<h4>FUTURE WORK</h4>
Because performance did not significantly improve with increased network complexity, improving accuracy would be better looked for by attempting to isolate which features are more important and dropping the less important ones from consideration.  Perhaps the cutoffs for binning into the Other category are too high in this work, and keeping more of the application and classification types separated from one another would be better.  Individual outliers could be removed from numerical columns, but this data set has a high portion of categorical data - perhaps some additional numerical data could be gathered about the funded ventures, such as number of people involved, number of years in operation, or by turning the INC_AMOUNT from ranges into exact, binned numerical values (each bin representing the middle of the associated range).
