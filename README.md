# Spoken_language_identification
Spoken_language_identification 
ProjectReport:Spoken Languageldentification 
Spoken Language Identification (SLI) is the process of determining the language spoken in an audio recording.In this project, we explore the use of Mel-Frequency Cepstral Coefficients (MFCC) and Convolutional Neural Networks (CNN) to identify the spoken language in audio fragments. The project involves 
data 
preprocessing,featureextraction using MFCC,modelbuildingusingCNN,andevaluationofthemodel'sperf 
ormance. 
CodeOverview 
• 
Data Preparation: The code starts by importing necessary libraries and loading the audio data using thesoundfilelibrary.Theaudiodataisread fromspecified pathsand loaded intoarrays. 
Feature Extraction: The code defines a function to generate Mel-Frequency Cepstral Coefficients(MFCC)fromaudiosignals. 
Thisfunction performspre- emphasis,framing,windowing, Fourier Transform, and calculatesfilterbanks. The MFCCfeaturesar ethenstandardized usingStandardScaler. 
• 
DataSplitting: Thedatasetissplitintotrainingandtestingsetsusingtrain_test_splitfromsklearn. 
• Model Architecture: A CNN model is defined using the Keras library. The model includes severalconvolutionaland poolinglayers, aswellasbatch normalizationanddropout layerstopreve 
• 
• 
ntoverfitting. 
Training: The model is compiled using appropriate loss and optimizer functions. The training processincludesusingalearningratescheduler,early stopping, and modelcheckpointing. 
Evaluation:Thetrained modelisevaluated usingthetestingdata.Performance metricssuchasaccu racyarecomputed, and classification reportsandconfusion matricesaregenerated. 
ErrorsandProblemswhilelmplementation 
• 
• 
• 
ValueError: when trying to split your dataset using the train_test_split function. The error messagesuggests that theresultingtrainset would beemptydue tothecombination ofyour parameters(n_samples=1, test_size=0.6, and train_size=None). This indicates that the 
dataset 
you're 
trying 
to 
splitmighthaveanissueortheremightbeamistakeinhowyou'reusingthetrain_test_splitfunction. 
Tryingtoperformatrain-testsplitusingthetrain_test_splitfunctionfromthescikit- 
learnlibrary.X_train is passed as the feature DataFrame, and X_train['language'] is used as the target variable(y_train)forthetrain-testsplit. 
FileNotFoundError: [Errno2] Nosuchfileordirectory:'../working/MFCC_data.npy',indicatesthatt hedirectory../working/doesnotexist, which iscausing thenp.save()functiontofail. 
generating MFCC features for your audio data and then storing these features in the MFCC_array.Inoticethatusingsc.fit_transform(MFCC)toapplyscalingoneachiterationoftheloop. Ifyouintendtousethesamescalerfortheentiredataset,youshouldfitthescaleroutsideoftheloopa 
ndthentransformeach iteration'sMFCCdata using thefittedscaler. 
• 
• 
Shapes of MFCC Array and Language Dummies: MFCC_array and language_dummies have compatibleshapesforsplitting.MFCC_arrayshouldhavetheshape(num_samples,num_features) wherenum_samples is the number of data points and num_features is the number of features 
in 
each 
MFCCarray.language_dummiesshouldhavetheshape(num_samples,num_classes)wherenum_ 
classesisthenumberofdifferentlanguageclasses. 
Matching Number of Samples: Number of samples in both MFCC_array and language_dummies match. The number of samples should be the same because you're performing a stratified split based on thelanguageclasses. 
The shapes ofMFCC_array and language_dummies arrays are not matching the expected dimensionsfor train-test splitting. The MFCC_array has a shape of (1, 1000, 40) and the language_dummies has ashapeof(1,1).Because I haveused a Personalized Dataseton thisproject. 
• 
FCC_arrayhasashapeof(1,1000,40)andyourlanguage_dummieshasashapeof(1,1). 
The issue seems to be that the dimensions of your arrays are not aligned properly for the train -test split.Let's reshape your arrays so that they match and then perform the split. Since i have only one sample ineach array,ineed to adjustthedimensionsaccordingly. 
language_dummies to have the same number of rows as MFCC_array. Since it seems you want to useone-hot encoded labels, you can replicate the single one-hot encoded row to match the number ofsamples. 
num_samples=MFCC_array.shape[0] 
language_dummies_expanded=np.repeat(language_dummies,num_samples,axis=0) 
Results 
The model's performance is evaluated using various metrics. The accuracy of the model on the testing datasetprovides insights into its generalization capabilities. The confusion matrix visualizes the model's 
performance 
inclassifyingdifferentlanguages.The projectalsoaimstoexploretheeffectsofhyperparameterssuchasthenum berofepochs, learning rate, and dropoutrateon the model'sperformance. 
Conclusion 
In this project, we successfully implemented a spoken language identification system using MFCC features andCNN. The model was trained and evaluated on a dataset containing audio fragments of different 
languages. 
Theperformancemetricsprovideinsightsintothemodel'saccuracyanditsabilitytoidentifyspokenlanguag es.Thisproject demonstrates the application of deep learning techniques in solving real-world problems like languageidentification. 
