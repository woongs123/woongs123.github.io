#Data Loading

    setwd("C:/data")
    boston <- read.table("housing.data", head=F, encoding="utf-8")
    
#Preserve raw
    
    boston_ <- boston
    boston_
    
#Assgin colnames
   
    colnames(boston_) <- c("CRIM", "ZN", "INDUS", "CHAS", "NOX", "RM", "AGE", "DIS", "RAD", "TAX", "PTRATIO", "B1000", "LSTAT", "MEDV")
    boston_
    boston_ <-as.data.frame(boston_)

#Training set, Test set split / Train : Test = 9 : 1 

    set.seed(7)
    train <- sample(nrow(boston_), nrow(boston_)*0.9) 
    boston_ <- boston_[train,] 
    boston_test <- boston_[-train,]
    boston_
    boston_test
