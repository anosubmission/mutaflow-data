MutaFlow Data
================ 

<span style="color:red;">BEWARE!</span>: The repository is very large due to the large amount of generated outputs. The extracted size is around 13.4GB.

This repository contains the data generated while performing the MutaFlow evaluation. The data is related to the paper [_**"Detecting Information Flow by Mutating Input Data"**_](https://dl.acm.org/citation.cfm?id=3155598&CFID=1005478616&CFTOKEN=50031448) presented at ASE 2017. The raw data of the evaluation plus some explaining spreadsheets is contained in an anonymized version in this repository.

In the following we explain the contents of the folders as well as how the data has to be read.

Due to technical reasons MutaFlow uses two different data output formats for the flow reports. The results are the same for both formats, one format additionally contains the name of the API method for both, the sink and the source.

MutaFlow Code
------------------

You can find the code here: [https://github.com/bjrnmath/mutaflow](https://github.com/bjrnmath/mutaflow)

MutaFlow: [Droidbench](https://github.com/secure-software-engineering/DroidBench) Evaluation
------------------------------------

We use the following naming scheme for log files:


* The file _"0\_Original.apk.pap"_ and _"0\_OriginalRef.apk.pap"_ in each folder contain the information of the non-mutated executions.

* The other files contain the information of the mutated executions, they are named as follows, separated by _"\_"_:
	1. Unique identifier
	2. API method name
	3. Location of the mutated source method in class (based on Jimple code)
	4. Class which contains the mutated source method call

We evaluated MutaFlow 10 times on Droidbench. Each "RunX" folder contains the following information:

* **Command\_line\_outputs**: 
	* Contains the data which was written to the command line by MutaFlow while running the application.
	* For each execution a _"\*\_out.txt"_ and a _"\*\_err.txt"_ is created, containing standard and error output respectively.
	* Contains also the data for some excluded applications of the final evaluation.
* **individual\_logs**:
	* Contains for each application the log created while an instrumented APK was executed. The reported flows are based on these logs. Also logs for some excluded applications are contained in here.
* **Flows\_per\_application.csv**:
	* Is _"tab"_ separated.
	* Contains the reported information flows for each Droidbench application.
	* Contains also the data for some excluded applications.
	* Remark: For the subject _"ActivityCommunication8"_ the extended output format was used, therefore the flow reports for this application additionally contain the name of the the API method for both, the sink and the source.

Additionally the top folder for DroidBench contains two files described below:

* **Times.csv**:
	* Is _"comma"_ separated.
	* Contains the instrumentation and execution time per application.
	* Each app was only instrumented once, since the instrumentation is deterministic.
	* Remark: For _run 4_ no execution time exists, since the file containing the times was corrupted. This had no effect on the remaining results of the run.
* **Verification.csv** 
	* Is _"comma"_ separated.
	* Contains the true positives, false positives and false negatives per application as defined by Droidbench (This means for example that a flow to _"putExtra"_ is not represented in the results even though it might be reported, if its not part of the Droidbench ground truth).

MutaFlow: Real World Applications Evaluation
-----------------------

We evaluated MutaFlow on 20 real world applications and ran the evaluation four times:

* **\*Application Name\* : \*Package Name\***

* Fabulous - Motivate Me! : co.thefabulous.app
* Adidas miCoach : com.adidas.micoach
* Fitness at Home : com.basti12354.minutesworkout
* Ab Workouts : com.bikiniabs
* 30 Day Fit Challenges Workout : com.davor.thirtydayfit
* BMI and Weight Tracker : com.despdev.weight\_loss\_calculator
* Calorie Counter - FDDB Extender : com.fddb
* Runkeeper - GPS Track Run Walk : com.fitnesskeeper.runkeeper.pro *this application was only executed once
* Kegel Trainer - Exercises : com.jsdev.pfei
* Test Diabetes sugar-Joke : com.MayersDev.TestedeDiabete
* Mysugr: Diabetes logbook : com.mysugr.android.companion
* Fitness Recipe of the day : com.OnVation.FitnessRecipeOfTheDay
* Abs workout 7 minutes : com.popularapp.abdominalexercise
* 7 Minute Workout : com.popularapp.sevenmins
* Calorie, Carb & Fat Counter : digifit.virtuagym.foodtracker
* Blood Pressure Log (bpresso) : com.freshware.bloodpressure
* Water Drink Reminder : com.northpark.drinkwater
* Lifesum: Healthy lifestyle : com.sillens.shapeupclub
* 30 Day Butt Challenge FREE : com.teerstudios.buttchallenge2
* Fast Calorie Counter : opunktschmidt.fastcaloriecounter

The folders and files contain the following information:

* **Command\_line\_outputs**: 
	* Contains the data which was written to the command line by MutaFlow while running the application.
	* For each execution a _"\*\_out.txt"_ and a _"\*\_err.txt"_ is created, containing standard and error output respectively.
	
* **individual\_logs**:
	* Contains for each application the log created by the instrumentation of MutaFlow. The reported flows are based on these logs.
	* Remark: Contains also the logs of _"com.fitnesskeeper.runkeeper.pro"_ that were generated after the ten-hour timeout. Only those logs that were generated in the ten-hour timeframe were considered in the evaluation.
		
* **Verified_Flows_X._Execution.ods**
	* Can be opened with [LibreOffice](https://de.libreoffice.org)
	* Contains the reported flows with the verification of the manual investigation for the _X_th run.
	
* **Locs\_and\_Times.csv**
	* Is _"comma"_ separated.
	* Contains the lines of code as well as the analysis time for MutaFlow on the real world applications.
	
We use the following naming scheme for log files:

* The file "_0\_Original.apk.pap_" and "_0\_OriginalRef.apk.pap_" in each _"individual\_logs"_ folder contains the log of the non-mutated executions.

* The other files contain the information of the mutated executions, they are named as follows, separated by _"\_"_:
	1. Unique identifier
	2. API method name
	3. Location of mutated source method in class (based on Jimple code)
	4. Class which contains the mutated source method call


[Flowdroid](https://github.com/secure-software-engineering/soot-infoflow-android): Droidbench Evaluation
--------------------------

* **individual\_logs**
	* Contains the command line output of Flowdroid per application. The end of the output contains the found flows.
	* Contains also the data for some excluded applications of the evaluation.
* **Verification\_and\_Times.csv**
	* Is _"comma"_ separated.
	* Contains true positives, false positives, the number of possible flows as defined by Droidbench (This means for example that a flow to _"putExtra"_ is not represented in the results even though it might be reported, if its not part of the Droidbench ground truth). Also, the execution time of Flowdroid per application is listed.
	
Flowdroid: Real World Applications Evaluation
--------------------------

* **individual\_logs**
	* Contains the command line output of Flowdroid per application. The end of the output contains the found flows.
	
* **Verified\_Flows\_Flowdroid.ods**
	* Can be opened with [LibreOffice](https://de.libreoffice.org)
	* Contains the reported flows with the verification of the manual investigation.
	
* **Locs\_and\_Times.csv**
	* Is _"comma"_ separated.
	* Contains the lines of code as well as the analysis time for Flowdroid on the real world applications.
