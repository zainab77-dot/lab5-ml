# lab5-ml
 Lab 5: Feature Engineering (Classification)
 
 
 
 name: zainab ibrahim alabdulal 
 
 id: 2240002182
### Lab focus
This dataset is already clean (no missing values, no duplicate rows, consistent data types). 

In this lab, we focus on **feature engineering** for a classification task.

### Objective
Build a baseline model to predict `Order_Status` (Delivered, Cancelled, In Transit) and learn how feature engineering choices affect model performance and feature importance. 
### Task
using the same dataset, change `top_k` in `Item_Name_reduced` (for example 3, 5, 6) and compare:
- accuracy
- top feature importances

## Trying Different Values for top_k

To reduce the cardinality of `Item_Name` (which has 9 unique values), 
I used frequency-based grouping — keeping the top-k most frequent items 
and replacing the rest with "Other". I experimented with three values.

---

**top_k = 3**

I started with top_k = 3, which reduced Item_Name from 9 unique values 
down to 4. The model achieved an accuracy of 0.4006. Delivered had the 
best recall at 0.54, while In Transit was completely missed (recall = 0.00).

![](Screenshot%202026-04-06%20172831.png)
![](Screenshot%202026-04-06%172855.png)
---

**top_k = 5**

Next, I tried top_k = 5, giving 6 unique values after reduction. 
This actually gave the worst accuracy of the three at 0.3882. 
Performance dropped slightly across all classes compared to top_k = 3, 
and In Transit was still not predicted at all.

[📷 insert screenshot — top_k=5 result]

---

**top_k = 6**

Finally, I tried top_k = 6, which gave 7 unique values. This achieved 
the best accuracy at 0.4034. Cancelled improved slightly to f1 = 0.43 
and Delivered reached f1 = 0.47. In Transit remained at recall = 0.00, 
which is likely due to class imbalance (only 998 samples vs ~2000 for 
the other classes).

[📷 insert screenshot — top_k=6 result]

---

**Conclusion**

top_k = 6 was selected as the final value. However, it is worth noting 
that Item_Name_reduced ranked very low in feature importance (~0.012), 
meaning this feature had minimal effect on the model overall. The dominant 
features were price_per_item, Delivery_Distance_km, and geographic 
coordinates.
