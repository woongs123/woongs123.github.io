#Data Loading

    setwd("C:/data")
    boston <- read.table("housing.data", head=F, encoding="utf-8")
    
#Preserve raw
    
    boston_ <- boston
    boston_
    
#assgin colnames
   
    colnames(boston_) <- c("CRIM", "ZN", "INDUS", "CHAS", "NOX", "RM", "AGE", "DIS", "RAD", "TAX", "PTRATIO", "B1000", "LSTAT", "MEDV")
    boston_
    boston_ <-as.data.frame(boston_)
