<h1>Boxplots of KEGG gene expression</h1>

<h2>👩🏻‍💻 Description</h2>
This repository contains scripts that visualizes KEGG gene expression data using boxplots from the ggplot2 library.
<br />

<h2>🪐 Languages and Libraries Used</h2>

- <b>R Markdown</b> 

The following package is required to run the scripts:
<br/>

```ruby
library(ggplot2)
```

<h2>🦠 boxplot.Rmd Walk-Through:</h2>
This script visualizes KEGG gene expression for species that survives/dies at temperature 37 Celsius using boxplots from the ggplot2 library.

<br/>
<br/>

 - Load the data frame and set temp 37 as factor:
 
 <br/>
 
```ruby
kegg <- read.delim("KEGG_37.txt",sep = " ",header = T)
#Set X37 as factor
kegg$X37_EVIDENCE <- as.character(kegg$X37_EVIDENCE)
kegg$X37_EVIDENCE <- as.factor(kegg$X37_EVIDENCE)
```

<br/>

- Run ggplot2 to get boxplot:
<br/>

<img width="966" alt="K19306" src="https://github.com/stellalo/boxplots/assets/89308696/2e75dd70-e4c8-482f-9558-4f5087b35fc2">

<h2>🦠 boxplot_pa.Rmd Walk-Through:</h2>
This script visualizes KEGG presence/absence for species that survive/dies at temperature 37 Celsius using boxplots from the ggplot2 library.

- To change the KEGG values from gene expression to presence/absence, convert any value greater than 0 to 1:

<br/>

```ruby
kegg[, -ncol(kegg)][kegg[, -ncol(kegg)] > 0] <- 1
kegg[, -ncol(kegg)][kegg[, -ncol(kegg)] <= 0] <- 0
```

- Example result:
<br/>

<img width="991" alt="K03767_pa" src="https://github.com/stellalo/boxplots/assets/89308696/cdc5bb16-38bf-48d2-b915-c04843ec6a3e">

<br/>

<h2>🦠 boxplot_OOB.Rmd Walk-Through:</h2>
This script visualizes the MeanErr of the RF training and testing data set using boxplots from the ggplot2 library.

<br/>
<br/>

```ruby
temp_oob_train <- read.delim("RF Loop Results/training_contingency.txt", sep = " ", header = T)
temp_oob_test <- read.delim("RF Loop Results/testing_contingency.txt", sep = " ", header = T)

temp <- data.frame(meanErr = c(temp_oob_train$MeanErr,temp_oob_test$MeanErr),type = c(rep("train", 100),rep("test",100)))

#Set type as factor
temp$type <- as.character(temp$type)
temp$type <- as.factor(temp$type)

#boxplot(temp_oob$train_MeanErr,temp_oob$test_MeanErr, names = c("train oob", "test oob"))
ggplot(data = temp, mapping = aes(x = type , y = meanErr)) + geom_boxplot() + labs(title = "Temp at 37")
```

- Example result:

<br/>
<img width="736" alt="boxplot_OOB_temp" src="https://github.com/stellalo/boxplots/assets/89308696/47c5ce3d-6d66-48f5-ab7d-cda694e0c93e">


