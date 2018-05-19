
We have run our scripts on the GPU server 13.90.81.78.

# To install the packages for running all the scripts execute the command-
pip3 install -r requirements.txt

# Raw data for cases and stock price change can be found at path-
    # Main Directory 
        /data/WorkData/firmEmbeddings/
        
    # Case Data is inside the directory
        CaseData/
        
    # Stock Data is inside the directory
        StockData/
        
# The data after processing and joining can be found at path - 
    # Main Directory 
        /data/WorkData/firmEmbeddings/Models/
        
    # Random Forest for Stock Prediction Data
         StockPredictionUsingRandomForest/
         
    # Neural Network for Stock Prediction Data
        StockPredictionUsingNeuralNetwork/
        
    # Neural Network for Firm Embeddings Data
        FirmEmbeddings/
        
        
# Script to process the raw case data is -
    Run the files in following order
      
    1.  filterCases.ipynb - Filters cases from sentences folder to get cases for category 6 and 7. It uses bb2topic.pkl, bb2genis.pkl, caseid_date.csv. The generates new folder Filtered_1 and following files are generated filtered.pkl, casedata.pkl. 

    2. ngramdataGenerate.ipynb - Filters bigram pickle files to get cases for category 6 and 7 . It uses casedata.pkl and [20180208]build_vocab_lemma_pos/phrased/ and creates new folder PickleFiles

    3. bigram.ipynb- It creates final ngramdata.pkl. The code uses id2gram.pkl, casedata.pkl, df-tf.pkl and files from PickleFiles folder

    4. doc2vec.py- Uses text from Filtered_1 and runs doc2vec algorithm on filtered cases and generate doc2vec_2.model

    5. modeltodata.ipynb - Uses casedata.pkl doc2vec_2.model and maps model vectors to case meta data and creates visualization of docvectors. The code produces following files docvector.pkl, traindocvector.pkl, testdocvector.pkl, validationdocvector.pkl


# Script to process the raw Stock Data is - 


# Script to join the two data sets - 

 
# Script to generate models  for stock prediction and firm embeddings -

    #Change file permissios to run the script
    chmod 755 RunAllmodels.sh
    
    # Run the following command to execute the script -
    sh RunAllmodels.sh
    
    This script contains three scripts. Path locations for the scripts on github are - 
    1. RunRandomForest.py is present in the directory Random_Forest/
    2. FirmEmbeddingsModel.py is present in the directory FirmEmbeddings/ 
    3. NeuralNetworkRun_3layers.py is present in the directory StockPrediction/
    
    The script RunRandomForest.py will generate the Random Forest model and it will also plot the graph for actual vs predicted change in stock price.
    
    
    The predictions on test data after running the NeuralNetworkRun_3layers.py script are saved in predictions.txt 
    in the same path from in which data is present. The file predictions.txt along with actual.txt (which is also present
    in the same path as predictions.txt) will be used by the notebook StockPrediction/ScatterPlotPredictedvsActual.ipynb 
    in plotting the actual/predicted stock price change. The notebook contains the absolute path for these files. Thus
    the notebook can also be run from anywhere on the GPU server.
    
    
    The firm embeddings matrix after running the script FirmEmbeddingsModel.py saves the matrix in the same path from 
    where data is present. This matrix will be used by FirmEmbeddings/VisualizeFirmsEmbeddings.ipynb to visualize the   embeddings. This notebook contains the tsne plots for category 6, 7 and combines cases. It also contains the embeddings visualization against industries of the firms, ranking of the firms, states in which they lie. The notebook also 
    contains cosine similarity plots for the two categories - Finance and Manufacturing. 

