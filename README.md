##Kaggle Titanic

Following the Kaggle Titanic tutorial located here: https://campus.datacamp.com/courses/kaggle-r-tutorial-on-machine-learning

I made this as future reference for myself. This is just the tutorial boiled down to it's essentials to get you from reading the test and train sets into RStudio (v1.0.153) to submission to Kaggle for scoring.

###Load train.csv, test.csv from https://www.kaggle.com/c/titanic/data
train <- read.csv("train.csv")
test <- read.csv("test.csv")

### import the rpart library
library(rpart)

###Build decision tree with rpart from train data
tree <- rpart(Survived ~ Pclass + Sex + Age + SibSp + Parch + Fare + Embarked, data=train, method="class")
This command is saying build a decision tree predicting Survived based on Pclass, Sex, Age, etc.
The tree can be visualized and labeled, respectively, with plot(tree) and text(tree)

###Use the decision tree to build predictions for the test data
prediction <- predict(tree, newdata=test, type="class")

###Add PassengerId to Survived predictions
solution <- data.frame(PassengerId = test$PassengerId, Survived = prediction)

###Create csv to submit to Kaggle
write.csv(solution, file = "solution.csv", row.names = FALSE)

###Upload to Kaggle
Predicting survival for the test set based on Pclass, Sex, Age, SibSp, etc. from the training set should give us a score of 0.78469.
