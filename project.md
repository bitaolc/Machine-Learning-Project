### Introduction

The goal of this project is to predict the manner in which parcipants
did the exercise by using data from accelerometers on the belt, forearm,
arm, and dumbell of 6 participants. More information is available at:
<http://web.archive.org/web/20161224072740/http:/groupware.les.inf.puc-rio.br/har>

### Reading and Cleaning Data

The training data set contains 19622 observations and 160 variables,
while the testing data set contains 20 observations and 160 variables.
The "classe" variable in the training set is the outcome to predict.
There are lots of variables in the training dataset that contain too
many NAs/ blank, so we need to check and remove them. The first 7
columns are not related to the result, so we will also remove them from
the training dataset.

After cleaning, the training dataset has 53 columns. Then split the
cleaned training set into a training data set (70%) and a validation
data set (30%). Since the test dataset is independent to the training
dataset, we would use the cross-validation techinique. It also offers
higher accuracy.

### Machine Learning Models

*Classification Tree*

The tree plot is shown as below:

![](https://github.com/bitaolc/Machine-Learning-Project/unnamed-chunk-2-1.png)

    Confusion Matrix and Statistics

            
    predict1    A    B    C    D    E
           A 1461  150   10   57   50
           B   88  814  138   68   71
           C   14  111  790  161   83
           D   44   56   47  643   82
           E   67    8   41   35  796

    Overall Statistics
                                              
                   Accuracy : 0.7653          
                     95% CI : (0.7543, 0.7761)
        No Information Rate : 0.2845          
        P-Value [Acc > NIR] : < 2.2e-16       
                                              
                      Kappa : 0.7028          
     Mcnemar's Test P-Value : < 2.2e-16       

    Statistics by Class:

                         Class: A Class: B Class: C Class: D Class: E
    Sensitivity            0.8728   0.7147   0.7700   0.6670   0.7357
    Specificity            0.9366   0.9231   0.9241   0.9535   0.9686
    Pos Pred Value         0.8455   0.6904   0.6816   0.7374   0.8405
    Neg Pred Value         0.9488   0.9309   0.9501   0.9360   0.9421
    Prevalence             0.2845   0.1935   0.1743   0.1638   0.1839
    Detection Rate         0.2483   0.1383   0.1342   0.1093   0.1353
    Detection Prevalence   0.2936   0.2003   0.1969   0.1482   0.1609
    Balanced Accuracy      0.9047   0.8189   0.8470   0.8102   0.8521

The accuracy of the classification tree model is 0.765, which is a
little bit lower. We need to try another model.

\newpage
*Random Forests*

    Confusion Matrix and Statistics

       predict2
           A    B    C    D    E
      A 1671    3    0    0    0
      B    4 1135    0    0    0
      C    0    7 1017    2    0
      D    0    0   10  953    1
      E    0    0    0    3 1079

    Overall Statistics
                                              
                   Accuracy : 0.9949          
                     95% CI : (0.9927, 0.9966)
        No Information Rate : 0.2846          
        P-Value [Acc > NIR] : < 2.2e-16       
                                              
                      Kappa : 0.9936          
     Mcnemar's Test P-Value : NA              

    Statistics by Class:

                         Class: A Class: B Class: C Class: D Class: E
    Sensitivity            0.9976   0.9913   0.9903   0.9948   0.9991
    Specificity            0.9993   0.9992   0.9981   0.9978   0.9994
    Pos Pred Value         0.9982   0.9965   0.9912   0.9886   0.9972
    Neg Pred Value         0.9991   0.9979   0.9979   0.9990   0.9998
    Prevalence             0.2846   0.1946   0.1745   0.1628   0.1835
    Detection Rate         0.2839   0.1929   0.1728   0.1619   0.1833
    Detection Prevalence   0.2845   0.1935   0.1743   0.1638   0.1839
    Balanced Accuracy      0.9984   0.9952   0.9942   0.9963   0.9992

![](project_files/figure-markdown_strict/unnamed-chunk-3-1.png)

The accuracy of the random forests model is 0.995. The expected
out-of-sample error is 100-99.49 = 0.51%. We will use it to predict the
values of classe for the test data set.

### Predicting Results and Conclusion

The classes of the 20 test cases are shown as following:

     1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 
     B  A  B  A  A  E  D  B  A  A  B  C  B  A  E  E  A  B  B  B 
    Levels: A B C D E

\newpage
### References

Ugulino, W.; Cardador, D.; Vega, K.; Velloso, E.; Milidiu, R.; Fuks, H.
Wearable Computing: Accelerometers' Data Classification of Body Postures
and Movements. Proceedings of 21st Brazilian Symposium on Artificial
Intelligence. Advances in Artificial Intelligence - SBIA 2012. In:
Lecture Notes in Computer Science. , pp. 52-61. Curitiba, PR: Springer
Berlin / Heidelberg, 2012. ISBN 978-3-642-34458-9. DOI:
10.1007/978-3-642-34459-6\_6.

Velloso, E.; Bulling, A.; Gellersen, H.; Ugulino, W.; Fuks, H.
Qualitative Activity Recognition of Weight Lifting Exercises.
Proceedings of 4th International Conference in Cooperation with SIGCHI
(Augmented Human '13) . Stuttgart, Germany: ACM SIGCHI, 2013.

Ugulino, W.; Ferreira, M.; Velloso, E.; Fuks, H. Virtual Caregiver:
Colaboração de Parentes no Acompanhamento de Idosos. Anais do SBSC 2012,
IX Simpósio Brasileiro de Sistemas Colaborativos , pp. 43-48. São Paulo,
SP: IEEE, 2012. ISBN 978-0-7695-4890-6.
