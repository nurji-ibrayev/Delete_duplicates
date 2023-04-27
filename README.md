# Delete_duplicates

![Screenshot](https://cdn-145.anonfiles.com/r2U3I3n2z7/36460069-1682585873/Screenshot_5.png "Dynamo screenshot")

# Python code
```
import clr
clr.AddReference('RevitAPI')
from Autodesk.Revit.DB import *
clr.AddReference('RevitNodes')
import Revit
clr.AddReference('RevitServices')
import RevitServices
from RevitServices.Persistence import DocumentManager
from RevitServices.Transactions import TransactionManager
#Введенные в этом узле данные сохраняется в виде списка в переменных IN.
Coordinates_list = IN[0]
IDs_list = IN[1]

Duplicates_ID = []
for i in range(len(Coordinates_list)):
  for j in range(i + 1, len(Coordinates_list)):  
    if j < len(Coordinates_list) and Coordinates_list[i] == Coordinates_list[j]: Duplicates_ID.append(IDs_list[j])
    else: pass
#Duplicates_ID = list(set(Duplicates_ID))

Document = DocumentManager.Instance.CurrentDBDocument
TransactionManager.Instance.EnsureInTransaction(Document)
Delete_duplicates = [Document.Delete(UnwrapElement(k).Id) for k in Duplicates_ID]
TransactionManager.Instance.TransactionTaskDone()
#Назначьте вывод переменной OUT.
OUT = Duplicates_ID
```
