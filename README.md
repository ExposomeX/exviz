# exviz: Exposome Visualization Module
### Author: Ning Gao (gaoning@pku.edu.cn)
### Date: 2022-12-02

The exviz package is designed for the data visualization of different statistical and biological analysis in a user friendly and easy way, including four typical classes of visualization. The visualization of the high dimension data is also very useful for the users in the field. The data visualization of different statistical analysis as well as the biological interaction can save much time for the data interpretation. Here, we mainly classify all the visualization task into four types, including category (distinguishing the characteristics of various groups), relationship (statistical relationship between various features), distribution  (the distribution characters of the single or multiple factors), and components (the inclusion relationship between the part components and the whole). For each type, users only need to provide the original dataset by following the template and the target types, the exviz package can generate various potential visualization types. Please see the website (http://www.exposomex.cn/#/expoviz) for more information. 

Users can install the package using the following code:

	if (!requireNamespace("devtools", quietly = TRUE)){

    	install.packages("devtools")
    
    	devtools::install_github('ExposomeX/exviz',force = TRUE)
    
    	devtools::install_github('ExposomeX/extidy',force = TRUE) #"extidy" package is optional if the data file has been well prepared. However, the it is recommended as users may need tidy the data to meet the modeling requirement, such as deleting varaibles with low variance, transforming data type, classifying variable into several level, etc.
	}

	library(exviz)
	library(extidy) 


### Tips:
1. Before using the package, a user defined physical output path (i.e., OutPath) is recommended. For example

		OutPath = "D:/test" #The default path is the current working directory of R. Users can use this code to set the preferred path.
		
2. For each step, the returned values can be named as users' like by following R language requirement. 

3. All the PID must be the same with the one provided by InitViz function, e.g., res$PID.


### Example codes:
##### 1. Initial Visualization module:
	res <- InitViz()
	res$PID
	
##### 2. Load data for visualization
	res2 <- LoadViz(PID=res$PID,
                  UseExample = "example#1",
		              DataPath = NULL,
		              VocaPath = NULL)
	res2$Expo$Data
	res2$Expo$Voca

##### 3 Set Output physical path (optional)
	OutPath = "E:/Viz_test" #The default path is the current working directory of R.
	
##### 4 Tidy procedures
	res3 = TransImput(PID=res$PID,
	                  Group="F",
	                  Vars="all.x",
	                  Method="lod")
	res4 = TransType(PID=res$PID,
	                 Vars="Y1",
	                 To="factor")
					 
	res5 = TransScale(PID=res$PID,
	                  Group="F",
	                  Vars="all.x",
	                  Method="normal")
	
	res6 = TransDistr(PID=res$PID,
	                  Vars="all.x",
	                  Method="ln")

##### 4. Plot category plot via dot plot
  res7 = VizCateDot(PID = res$PID,
                    Group = "F",
                    Vars = "X4,X5,X6,X7,X8,X9,X10",
                    Parameter = "mean",
                    Brightness = "light",
                    Palette = "default1")
  res7$Cate_Dot$light_default1

##### 5. Plot relationship plot via network plot
	res8 = VizRelatNetwork(PID = res$PID,
                         VarsY = "Y2",
                         VarsC = "all.c",
                         VarsX = "all.x",
                         Family = "gaussian",
                         Layout = "force-directed",
                         CutOff = 0.8,
                         Brightness = "light",
                         Palette = "default1")
	res8$Relat_Network$light_default1

##### 6. Plot relationship plot via edge bundling plot
	res9 = VizRelatEdgeBundling(PID = res$PID,
                              OutPath = "default",
                              VarsY = "Y2",
                              VarsC = "all.c",
                              VarsX = "all.x",
                              Family = "gaussian",
                              SizeFor = "pvalue",
                              Brightness = "light",
                              Palette = "default1")
	res9$Relat_Edgebundling$light_default1

##### 7. Plot relationship plot via heatmap plot
	res10 = VizRelatHeatmap(PID = res$PID,
                          OutPath = "default",
                          Group = "F",
                          VarsY = "Y2",
                          VarsX = "X4,X5,X6,X7,X8,X9",
                          Method = "spearman",
                          Brightness = "light",
                          Palette = "default1")
res10$Relat_Heatmap$light_default1

##### 8. Plot relationship plot via matrix plot
	res11 = VizRelatMatrix(PID = res$PID,
                         OutPath = "default",
                         Group = "F",
                         VarsY = "Y2",
                         VarsX = "X1,X4,X5,X6,X7,X8,X9,X10",
                         Method = "spearman")
res11$Relat_Matrix$ALL

##### 9. Plot distribution plot via sierra plot
	res12 = VizDistrSierra(PID=res$PID,
                         OutPath="default",
                         Group = "F",
                         Vars = "X14,X15,X16,X17,X18,X19,X20",
                         Brightness = "light",
                         Palette = "default1")
  res12$Sierra$light_default1

##### 10. Plot component plot via dendrogram plot
	res13 = VizCompoDendrogram(PID = res$PID,
                             OutPath = "default",
                             Group = "T",
                             Vars = "X4,X5,X6,X7,X8,X61,X66,X67,X200",
                             Parameter = "median",
                             DistMethod = "euclidean",
                             ClusterMethod = "ward.D2",
                             ClusterNum = "4",
                             Brightness = "light",
                             Palette = "default1")
res13$Dendrogram$all_light_default1

##### 11. Exit
	FuncExit(PID = res$PID)
