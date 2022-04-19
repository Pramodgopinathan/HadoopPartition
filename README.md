# Why we need to do partitioning in map reduce ??
As you must be aware that a map reduce job takes an input data set and produces the list of key value paire(Key,value) which is a result of map phase in which the input data set is split and each map task processs the split and each map output the list of key value pairs.
The output from map are then feed to reduce tasks which processes the user defined reduce function on map outputs. But before the reduce phase is another process that partition the map outputs based on the key and it keeps the record of same key into the same partitions.

Let's say i have an data set of the form person information,Our dataset contains the name,country, sports liked(To keep it simple i have used three fields).

PersonA,India,Cricket </br>
PersonB,Brazil,Soccer</br>
PersonC,Australia,Baseball</br>
PersonD,India,Cricket</br>
PersonE,England,Cricket</br>
PersonF,Australia,Cricket</br>
PersonG,India,Cricket</br>
PersonH,England,Cricket</br>
PersonI,India,Cricket</br>
PersonJ,India,Cricket</br>
PersonK,India,Cricket</br>

We need to count the person for each of the game in the list. 
So our key becomes the third field i.e., the game</br>

So all values with same key(cricket) send to same reducer. but since our data contains a large number of such key value pair due the fact the country frequency of dataset is india.</br>

And also data key (cricket) is also present for other country map output. So we have a lots of key value data to send to same reducer for cricket key. Here we will write our custom partitioner. And follows the approach below.</br></br></br>

 

Our custom partitioner will send all key value by country india to one partition and other key value with countries like(England,Australia) to other partition so that work load one reducer that should process key cricket is divided into two reducers. </br></br>

 
