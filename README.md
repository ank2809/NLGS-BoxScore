# NBA Game Summary Generation from Box Scores and Contextual Player/Team Information – Select and Generate
# Ansh Kothary, ank2145

All of the code is in the Python notebook and can be run from the notebook or from Google Colab linked in the notebook. I have divided the notebook into sections. For every section you want to run, you must run all the cells in that section (minus any output cells marked as optional).

These are the sections (which are later referenced in the core codepaths) -

1. Data Processing: This section must be run for any part of the model to work. You can change the argument passed from 'rotowire' to 'sbnation' depending on which dataset you want to use. Make sure the path points to the correct place.
2. Create Static Data: This section is optional and should only be run if we want to include static data in both stages of the model. If it is to be used, all cells in this section must be run.
3. Create Dynamic Data: This section is optional and should only be run if we want to include dynamic data in the second stage of the model. If it is to be used, all cells in this section must be run.
4. Stage 1 of Model (SELECT): This section includes the specific pre-processing and running of the first stage of the model. Both stages of the model can be trained and evaluated independently. This stage includes the binary classifier to pick which rows of the box_score should be included in the summary.
5. Stage 2 of Model (GENERATE): This section includes the specific pre-processing and running of the second stage of the model. Both stages of the model can be trained and evaluated independently. This stage includes the pre-trained large language model to generate text from a given box score.

This stage includes the binary classifier to pick which rows of the box_score should be included in the summary

These are the core codepaths -

* Data Downloading: https://github.com/harvardnlp/boxscore-data. This is the GitHub repo containing the RotoWire (professional) and SBNation (fan-written) game summaries. By default I use RotoWire, but you change the argument at the beginning of the notebook
* Data Processing: Section 1 of the Notebook (from above) must be run before anything else. It will handle all data processing and create the core datasets.
* Training Baselines: To train the baselines of the model, run only Section 1 along with Section 4 and 5. By not including Section 2 and 3, the model is trained only on pure box score data with no contextual data. You can train baselines for Stage 1 of the model in Section 4 and Stage 2 of the model in Section 5.
* Training Extensions: The main extension is using contextual data. To do this run Section 1, along with one or both of Section 2 and 3. Then train Stage 1 of the model in Section 4 and Stage 2 of the model in Section 5. To test the other extension of using SBNation ahead of RotoWire, replace the 'rotowire' argument in Section 1 with 'sbnation' and then train Section 4 and 5.
* Evaluating Results: I have not decoupled evaluation and training. By default when you train the model, it will automatically do an 80/20 split and evaluate the results on the 20% (this is true for both sections).
* Sampling: There is no sampling for Stage 1 (binary classifier). After training and evaluation, you can sample some results from the test set of Stage 2, by running the last cell in Section 5.2.
