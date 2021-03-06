-----------------------
Div400 - Dataset readme
-----------------------

----------
**Authors: 
Bogdan Ionescu, LAPI, University Politehnica of Bucharest, Romania(bogdanLAPI@gmail.com); 
María Menéndez, KnowDive, Department of Information Engineering and Computer Science, University of Trento, Italy (menendez@disi.unitn.it); 
Henning Müller, University of Applied Sciences Western Switzerland (HES-SO) in Sierre, Switzerland (henning.mueller@hevs.ch);
Adrian Popescu, CEA LIST, France (popescu_adi@yahoo.co.uk).

This dataset was supported by the following projects: EXCEL POSDRU, CUbRIK, PROMISE and MUCKE. Many thanks to Anca-Livia Radu, Bogdan Boteanu, Ivan Eggel, Sajan Raj Ojha, Ionuț Mironică, Ionuț Dută, Oana Pleș, Andrei Purică, Macovei Corina and Irina Nicolae for their help.


----------
**Citation:
B. Ionescu, M. Menéndez, H. Müller, A. Popescu, “Retrieving Diverse Social Images at MediaEval 2013: Objectives, Dataset and Evaluation”, MediaEval Benchmarking Initiative for Multimedia Evaluation, vol. 1043, CEUR-WS.org, ISSN: 1613-0073, October 18-19, Barcelona, Spain, 2013.



----------
**Description:
The dataset consist of a set of 396 locations that are divided into a development set containing 50 locations (devset) and a test set containing 346 locations (testset).

Each of the two data sets contains data that was retrieved from Flickr using the name of the location as query (denoted keywords) and data that was retrieved using the name of the location and the GPS coordinates (denoted keywordsGPS). 

For each location, we provide the following information:
-location name: is the name of the location and represents its unique identifier;
-location name query id: unique numeric identifier (i.e., numbers from 1 to 396 - the total number of locations - 1 to 50 is belonging to the devset locations and the rest to the testset locations);
-GPS coordinates: latitude and longitude in degrees;
-link to the Wikipedia webpage of the location;
-a representative photo retrieved from Wikipedia in jpeg format;
-a set of photos retrieved from Flickr in jpeg format (up to 150 photos per location - each photo is named according to its unique id from Flickr). Photos are stored in individual folders named after the location name;
-an xml file containing metadata from Flickr for all the retrieved photos;
-visual and textual descriptors;
-ground truth for both relevance and diversity.


---Important--: please note that all the photos provided are under Creative Commons licenses. Each Flickr photo is provided with the license type and the owner's name. For the Wikipidia photos the owner name is included in the photo file name, e.g., for “Basilica of Saint Peter Vatican (Wolfgang Stuck).jpg” the owner name is Wolfgang Stuck. 



----------
**XML metadata
Each location is accompanied by an xml file (UTF-8 encoded) that contains all the retrieved metadata for all the photos. Each file is named after the location name, e.g., “Basilica of St Mary of Health Venice.xml”. The information is structured as follows:

<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<photos monument="Basilica of St Mary of Health Venice">
<photo date_taken="2003-10-09 15:19:30" description="The Basilica di Santa Maria della Salute (Basilica of St Mary of Health/Salvation), commonly known simply as the Salute, is a famous church in Venice, placed scenically at a narrow finger of land which lies between the Grand Canal and the Bacino di San Marco on the lagoon, visible as one enters the Piazza San Marco from the water. (Wikipedia)" id="2323210481" latitude="0" license="3" longitude="0" nbComments="50" rank="1" tags="europe italy venice basilicadisantamariadellasalute basilicaofstmaryofhealthsalvation grandcanal sunrise church basilica travel sony f717" title="Basilica of St Mary of Health/Salvation, Venice" url_b="http://static.flickr.com/2410/2323210481_31da0f0311_b.jpg" username="Christopher Chan" views="6824"/>
...
</photos>

The monument value is the unique location name identifier mentioned in the data set list. Then, each of the photos are delimited by a <photo /> statement. Among the photo information fields, please note in particular:
-description contains a detailed textual description of the photo as provided by author;
-id is the unique identifier of each photo from Flickr and corresponds to the name of the jpeg file associated to this photo (e.g., “2323210481.jpg”); 
-license is the Creative Common license of this picture; 
-nbComments is the number of comments posted on Flickr about this photo;
-rank is the position ranking of the photo in the list retrieved from Flickr;
-tags are the tag keywords used for indexing purpose;
-title is a short textual description of the photo provided by the author;
-url_b is the url link of the photo location from Flickr (please note that by the time you use the dataset some of the photos may not be available anymore at the same location);
-username represent the photo owner’s name;
-views is the number of times the photo has been displayed on Flickr.



---------- 
**Visual descriptors
For each location and photo, we provide some general purpose visual descriptors, namely:
-Global Color Naming Histogram (code CN - 11 values): maps colors to 11 universal color names: “black”, “blue”, “brown”, “grey”, “green”, “orange”, “pink”, “purple”, “red”, “white”, and “yellow” [v1];
-Global Histogram of Oriented Gradients (code HOG - 81 values): represents the HoG feature computed on 3 by 3 image regions [v2];
-Global Color Moments on HSV Color Space (code CM - 9 values): represent the first three central moments of an image color distribution: mean, standard deviation and skewness [v3];
-Global Locally Binary Patterns on gray scale (code LBP - 16 values) [v4];
-Global Color Structure Descriptor (code CSD - 64 values): represents the MPEG-7 Color Structure Descriptor computed on the HMMD color space [v5];
-Global Statistics on Gray Level Run Length Matrix (code GLRLM – 44 dimensions): represents 11 statistics computed on gray level run-length matrices for 4 directions: Short Run Emphasis (SRE), Long Run Emphasis (LRE), Gray-Level Non-uniformity (GLN), Run Length Non-uniformity (RLN), Run Percentage (RP), Low Gray-Level Run Emphasis (LGRE), High Gray-Level Run Emphasis (HGRE), Short Run Low Gray-Level Emphasis (SRLGE), Short Run High Gray-Level Emphasis (SRHGE), Long Run Low Gray-Level Emphasis (LRLGE), Long Run High Gray-Level Emphasis (LRHGE) [v6];
-Spatial pyramid representation (code 3x3): each of the previous descriptors is computed also locally. The image is divided into 3 by 3 non-overlapping blocks and descriptors are computed on each patch. The global descriptor is obtained by the concatenation of all values.

File format. Visual descriptors are provided on a per location basis. We provide individual csv (comma-separated values) files for each type of visual descriptor and for each location. The naming convention is the following: location name followed by the descriptor code, e.g., “Abbey of Saint Gall CM3x3.csv” refers to the Global Color Moments (CM) computed on the spatial pyramid (3x3) for the location Abbey of Saint Gall. Each file contains the descriptors for each of the photos of the location on one line. The first value of each line is the unique photo id followed by the descriptor values separated by commas. Lines are separated by an end-of-line character (carriage return). An example is presented below:

3338743092,0.51934475780470812,0.40031641870181739,...
3338745530,0.20630411506897756,0.26843536114050304,...
3661394189,0.47248077522064869,0.17833862284689939,...
...

In particular, we provide the visual descriptors also for the Wikipedia representative photos. In this case descriptors are provided on a per data set basis. We provide individual csv (comma-separated values) files for each type of visual descriptor and for each data set (keywords, keywordsGPS for devset and testset).

The files are named according to the data set followed by the descriptor code, e.g., “devsetkeywordsGPS-CM3x3.csv” refers to the Global Color Moments (CM) computed on the spatial pyramid (3x3) for the devset retrieved using keywords and GPS. Each file contains the descriptors for each of the Wikipedia photo of the current data set on one line. The first value of each line is the Wikipedia photo file name followed by the descriptor values separated by commas. Lines are separated by an end-of-line character (carriage return). An example is presented below:

Abbey of Saint Gall (Pjetter),0.387094,0.208926,...
Basilica of Saint Peter Vatican (Wolfgang Stuck),0.410299,0.283104,...
Basilica of St Mary of Health Venice (Radomil),0.492273,0.385439,...
...



----------
**Textual descriptors
We provide three types of textual models that were created using tag and title words of the Flickr metadata. A list of English stop words was used to exclude them from the models. Single character words were also removed. We extracted the following models:
-probabilistic model (code probabilistic): estimates the probability of association between a word and a given location by dividing the probability of occurrence of the word in the metadata associated to the location by the overall occurrences of that word [t1];
-TF-IDF weighting (code tfidf): term frequency–inverse document frequency is a numerical statistic which reflects how important a word is to a document in a collection or corpus. The tf-idf value increases proportionally to the number of times a word appears in the document, but is offset by the frequency of the word in the corpus, which helps to control for the fact that some words are generally more common than others [t2];
-Social TF-IDF weighting (code social-tfidf): is an adaptation of TF-IDF to the social space (documents with several identified contributors). It exploits the number of different users that tag with a given word instead of the term count at document level and the total number of users that contribute to a document's description. At the collection level, we exploit the total number of users that have used a document instead of the frequency of the word in the corpus. This measure aims at reducing the effect of bulk tagging (i.e., tagging a large number of photographs with the same words) and to put forward the social relevancy of a term through the use of the user counts [t3];

All three models use the entire collection (devset and testset) to derive term background information, such as the total number of occurrences for the probabilistic model, the inverse document frequency for tf-idf or the total number of users for social_tfidf.

File format. Textual descriptors are provided on a per data set basis. We provide individual txt files for each type of textual descriptor and for each data set (keywords, keywordsGPS for devset and testset). The files are named according to the data set followed by the descriptor code, e.g., “devsetkeywordsGPS-social-tfidf.txt” refers to the Social TF-IDF weighting (social-tfidf) for the devset retrieved using keywords and GPS.
 
Each file contains a line for each location in the current data set representing the model for that location. Columns are separated by tabulations. The first column of the line is the location name and the other columns contain each related word and its associated weight. Associated words are sorted by decreasing scores. An example is presented below:

Acropolis of Athens     athens 4.40528452733166 acropolis 4.20622678142275   greece 3.76325594440392  parthenon 2.2610684290111    erechtheion 1.52875073025019 caryatids 1.42927739744005  erechtheum 1.22546479160142  porch 0.813385624755926 ancient 0.813002286556494 ????? 0.793108190858887 ruins 0.781809082702648 europe 0.712768973519344      temple 0.703663092211997     athina 0.67812363924976 dionysus 0.542498911399808      grecia 0.542498911399808     athena 0.528738793905925     atticus 0.528738793905925      herodes 0.528738793905925    athenes 0.435788841498874    atenas 0.435788841498874     
...
Teatro Colon teatro 3.7848457361437        colón 3.22930179824282      buenosaires 3.03586015008148            argentina 2.62184141085557            teatrocolón 2.61212765739044         buenos 1.82393823658931    aires 1.82393823658931    colon 1.82077900997113      teatrocolon 1.44947359019038         theatre 1.07309598120772            southamerica 0.845815205236367    operahouse 0.731178058898631       capitalfederal 0.72473679509519            theater 0.704644004740362  colontheatre 0.558924228132525     plazalavalle 0.558924228132525      vitral 0.511120974300805  cúpula 0.483157863396793   julio 0.447928510033621
...

 

----------
**Topic files
For each sub-dataset we provide a topic file that contains the list of the locations in the current dataset. Each location is delimited by a <topic> </topic> statement and includes the query id code (delimited by a <number> </number> statement), the name of the location (delimited by a <title> </title> statement), the GPS coordinates (latitude and longitude in degrees) and the url to the Wikipedia webpage (delimited by a <wiki> </wiki> statement). An example is presented below:

<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<topics>
<topic>
    <number>26</number>
    <title>Abbey of Saint Gall</title>
    <latitude>47.423056</latitude>
    <longitude>9.377222</longitude>
    <wiki>http://en.wikipedia.org/wiki/Abbey_of_Saint_Gall</wiki>
</topic>
...
</topics>



----------
**Ground truth
The ground truth data consists on relevance ground truth (code rGT) and diversity ground truth (code dGT and dclusterGT). Ground truth was generated by a small group of expert annotators with advanced knowledge of location characteristics. In addition to the expert generated ground truth, we also provide a crowd-sourcing ground truth for a selection of 50 locations from the testset.  

Relevance ground truth was annotated using a dedicated tool that provided the annotators with one photo at a time. A reference photo of the location could be also displayed during the process. Annotators were asked to classify the photos as being relevant (score 1), non-relevant (score 0) or with “don’t know” answer (score -1). The definition of relevance was available to the annotators in the interface during the entire process. The annotation process was not time restricted. Annotators were recommended to consult any additional information about the characteristics of the location (e.g., from Internet) in case they were unsure about the annotation.

Ground truth was collected from several annotators and final ground truth was determined after a majority voting scheme.

File format. Ground truth is provided on a per location basis. We provide individual txt files for each location. Files are named according to the location name followed by the ground truth code, e.g., “Abbey of Saint Gall rGT.txt” refers to the relevance ground truth (rGT) for the location Abbey of Saint Gall. Each file contains photo ground truth on individual lines. The first value of each line is the unique photo id followed by the ground truth value separated by comma. Lines are separated by an end-of-line character (carriage return). An example is presented below:

3338743092,1
3338745530,0
3661394189,1
...


Diversity ground truth was also annotated with a dedicated tool. The diversity is annotated only for the photos that were judged as relevant in the previous step. For each location, annotators were provided with a thumbnail list of all the relevant photos. The first step required annotators to get familiar with the photos by analyzing them for about 5 minutes. Next, annotators were required to re-group the photos into similar visual appearance clusters. Full size versions of the photos were available by clicking on the photos. The definition of diversity was available to the annotators in the interface during the entire process. For each of the clusters, annotators provided some keyword tags reflecting their judgments in choosing these particular clusters. Similar to the relevance annotation, the diversity annotation process was not time restricted.

In this particular case, ground truth was collected from several annotators that annotated distinct parts of the data set (the exact numbers are provided in the corresponding Development Data and Test Data sections below).

File format. Ground truth is provided on a per location basis. We provide two individual txt files for each location: one file for the cluster ground truth and one file for the photo diversity ground truth. Files are named according to the location name followed by the ground truth code, e.g., “Abbey of Saint Gall dclusterGT.txt” and “Abbey of Saint Gall dGT.txt” refer to the cluster ground truth (dclusterGT) and photo diversity ground truth (dGT) for the location Abbey of Saint Gall.
 
In the dclusterGT file each line corresponds to a cluster where the first value is the cluster id number followed by the cluster user tag separated by comma. Lines are separated by an end-of-line character (carriage return). An example is presented below:

1,outside statue
2,inside views
3,partial frontal view
4,archway
...

In the dGT file the first value on each line is the unique photo id followed by the cluster id number (that corresponds to the values in the dclusterGT file) separated by comma. Each line corresponds to the ground truth of one image and lines are separated by an end-of-line character (carriage return). An example is presented below:

3664415421,1
3665220244,1
...
3338745530,2
3661396665,2
...
3662193652,3
3338743092,3
3665213158,3
...



----------
**MediaEval submission format

The following information will help reproducing the exact evaluation conditions of the MediaEval task. At MediaEval runs were provided in the form of a trec topic file. This file is compatible with the trec_eval evaluation software (for more information please follow the previous link – you will find two archives trec_eval.8.1.tar.gz and trec_eval_latest.tar.gz - see the README file inside). The trec topic file has the structure illustrated by the following example of a file line (please note that values are separated by whitespaces):

030 Q0 ZF08 0 4238 prise1
qid iter docno rank sim run_id

where:
-qid is the unique query id (please note that each location name has a certain query id code that is provided with the data set in the topic xml files); 
-iter – is ignored; 
-docno – is the unique photo id (as provided with the data set); 
-rank – is the photo rank in the refined list provided by your method. Rank is expected to be an integer value ranging from 0 (the highest rank) up to 49; 
-sim – is the similarity score of your photo to the query and is mandatory for the submission. The similarity values need to be higher for the photos to be ranked first and should correspond to your refined ranking (e.g., the photo with rank 0 should have the highest sim value, followed by photo with rank 1 with the second highest sim value and so on). In case your approach do not provide explicitly similarity scores (e.g., crowd-sourcing) you are required to create dummy similarity scores that decrease when the rank increases (e.g., in this case, you may use the inverse ranking values); 
-run_id - is the name of your run (which you can choose, but should be as informative as possible without being too long – please note that no whitespaces or other special characters are allowed);

Please note that each run needs to contain at least one result for each location. An example of results file should look like this:

1 0 3338743092 0 0.94 run1_audiovisualRF
1 0 3661411441 1 0.9 run1_audiovisualRF
...
1 0 7112511985 48 0.2 run1_audiovisualRF
1 0 711353192 49 0.12 run1_audiovisualRF
2 0 233474104 0 0.84 run1_audiovisualRF
2 0 3621431440 1 0.7 run1_audiovisualRF
...


  
----------
**Scoring tool 
The official MediaEval scoring tool is div_eval.jar. It computes cluster recall at X (CR@X --- a measure that assesses how many different clusters from the ground truth are represented among the top X results), precision at X (P@X --- measures the number of relevant photos among the top X results) and their harmonic mean, i.e., F1-measure@X (X in {5,10,20,30,40,50}).

The software tool was developed under Java and to run it you need to have Java installed on your machine. To check, you may run the following line in a command window: "java -version". In case you don't have Java installed, please visit this link, download the Java package for your environment and install it.

To run the script, use the following syntax (make sure you have the div_eval.jar file in your current folder):

java -jar div_eval.jar -r <runfilepath> -rgt <rGT directory path> -dgt <dGT directory path> -t <topic file path> -o <output file directory> [optional: -f <output file name>]

where:
-r <runfilepath> - specifies the file path to the current run file for which you want to compute the evaluation metrics;
-rgt <rGT directory path> - specifies the path to the relevance ground truth (denoted by rGT) for the current data set;
-dgt <dGT directory path> - specifies the path to the diversity ground truth (denoted by dGT) for the current data set;
-t <topic file path> - specifies the file path to the topic xml file for the current data set;
-o <output file directory> - specifies the path for storing the evaluation results. Evaluation results are saved as .csv files (comma separated values);
-f <output file name> - is optional and specifies the output file name. By default, the output file will be named according to the run file name + "_metrics.csv".

Run example:

java -jar div_eval.jar -r c:\divtask\RUNd2.txt -rgt c:\divtask\rGT -dgt c:\divtask\dGT -t c:\divtask\devsetkeywordsGPS_topics.xml -o c:\divtask\results –f my_first_results

Output file example (for the devset keywordsGPS data set):

--------------------
"Run name","RUNd2.txt"
--------------------
"Average P@10 = ",.784
"Average CR@10 = ",.4278
"Average F1@10 = ",.5432
--------------------
"Query Id ","Location name",P@5,P@10,P@20,P@30,P@40,P@50,CR@5,CR@10,CR@20,CR@30,CR@40,CR@50,F1@5,F1@10,F1@20,F1@30,F1@40,F1@50
1,"Aachen Cathedral",.8,.9,.95,.9667,.95,.94,.1333,.4,.5333,.7333,.8667,.9333,.2286,.5538,.6831,.834,.9064,.9367
2,"Angel of the North",1.0,.9,.95,.9333,.925,.94,.2667,.5333,.8,.8667,.8667,.9333,.4211,.6698,.8686,.8988,.8949,.9367
...
24,"Acropolis of Athens",.6,.8,.85,.8667,.875,.88,.25,.5,.6667,.6667,.8333,.8333,.3529,.6154,.7473,.7536,.8537,.856
25,"Ernest Hemingway House",.8,.7,.5,.5667,.55,.6,.2353,.4118,.5294,.6471,.7647,.8824,.3636,.5185,.5143,.6042,.6398,.7143
--------------------
"--","Avg.",P@5,P@10,P@20,P@30,P@40,P@50,CR@5,CR@10,CR@20,CR@30,CR@40,CR@50,F1@5,F1@10,F1@20,F1@30,F1@40,F1@50
,,.76,.784,.792,.784,.789,.7944,.2577,.4278,.6343,.7443,.8504,.8919,.376,.5432,.696,.757,.813,.834



----------
**References:
[v1] Van de Weijer, C. Schmid, J. Verbeek, D. Larlus, „Learning color names for real-world applications”, IEEE Trans. on Image Processing, 18(7), pp. 1512-1523, 2009.
[v2] O. Ludwig, D. Delgado, V. Goncalves, U. Nunes: ”Trainable Classifier-Fusion Schemes: An Application To Pedestrian Detection”, Conference On Intelligent Transportation Systems, 2009.
[v3] M.Stricker, M. Orengo, “Similarity of color images”, SPIE Conference on Storage and Retrieval for Image and Video Databases III, vol. 2420, pp. 381­392, Feb. 1995.
[v4] T. Ojala, M. Pietikäinen, D. Harwood, “Performance evaluation of texture measures with classification based on Kullback discrimination of distributions”, IAPR International Conference on Pattern Recognition, vol. 1, pp. 582 – 585, 1994.
[v5] B. S. Manjunath, J. R. Ohm, V. V. Vasudevan, A. Yamada, “Color and texture descriptors”, IEEE Transactions on Circuits and Systems for Video Technology, vol. 11(6), pp. 703-715, 2001.
[v6] X. Tang, ”Texture Information in Run-Length Matrices”, IEEE Transactions on image Processing, vol.7(11), 1998.
[t1] J.M. Ponte, W.B. Croft, „A Language Modeling Approach to Information Retrieval”,  Research and Development in Information Retrieval. pp. 275–281, 1998.
[t2] G. Salton, M.J. McGill, „Introduction to modern information retrieval”, McGraw-Hill, Inc. New York, NY, USA, ISBN:0070544840, 1986.
[t3] A. Popescu, G. Grefenstette, „Social Media Driven Image Retrieval”, ACM International Conference on Multimedia Retrieval, April 17 - 20, Trento, Italy, 2011.


