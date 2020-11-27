### Data Loading

    setwd("C:/data")
    boston <- read.table("housing.data", head=F, encoding="utf-8")
    
### Preserve Raw file
    
    boston_ <- boston
    boston_
    
### Assgin colnames
   
    colnames(boston_) <- c("CRIM", "ZN", "INDUS", "CHAS", "NOX", "RM", "AGE", "DIS", "RAD", "TAX", "PTRATIO", "B1000", "LSTAT", "MEDV")
    boston_
    boston_ <-as.data.frame(boston_)

---

### Training set, Test set split / Train : Test = 9 : 1 
![image](https://user-images.githubusercontent.com/74387174/100453149-d39be300-30fd-11eb-959c-9a9ce7aec9eb.png)

    set.seed(7)
    train <- sample(nrow(boston_), nrow(boston_)*0.9) 
    boston_ <- boston_[train,] 
    boston_test <- boston_[-train,]
    boston_
    boston_test
    
---
### Linear regression model assumption check - Normality of Residuals 

    setwd("C:/data")
    boston_raw <- read.table("housing.data", head=F, encoding="utf-8")
    colnames(boston_raw) <- c("CRIM", "ZN", "INDUS", "CHAS", "NOX", "RM", "AGE", "DIS", "RAD", "TAX", "PTRATIO", "B1000", "LSTAT", "MEDV")


### Box-cox transformation y

    boston_raw_bc <- boston_raw
    library(MASS)
    box_df <- boxcox(boston_raw_bc$MEDV~1)
    lam <- box_df$x[which.max(box_df$y)]
    boston_raw_bc$MEDV_ <- (boston_raw_bc$MEDV^lam-1)/lam
    ks.test(boston_raw_bc$MEDV_, "pnorm", mean= mean(boston_raw_bc$MEDV_), sd = sd(boston_raw_bc$MEDV_))
    
### MEDV vs SQRT(MEDV) vs BOXCOX(MEDV)

    ggplot(boston_raw,aes(x=MEDV)) + geom_histogram(bins=50)
    ggplot(boston_raw,aes(x=sqrt(MEDV))) + geom_histogram(bins=50)
    ggplot(boston_raw_bc,aes(x=MEDV_)) + geom_histogram(bins=50)
### MEDV
![image](https://user-images.githubusercontent.com/74387174/100452718-098c9780-30fd-11eb-9e5b-0664c3a94b2f.png) 

### SQRT(MEDV)
![image](https://user-images.githubusercontent.com/74387174/100452758-1a3d0d80-30fd-11eb-8258-3f1d91524d89.png) 

### BOXCOX(MEDV)
![image](https://user-images.githubusercontent.com/74387174/100452770-232ddf00-30fd-11eb-87bd-feb1d898f2af.png)

---

