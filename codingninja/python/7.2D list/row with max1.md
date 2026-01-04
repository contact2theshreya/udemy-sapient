<img width="426" height="401" alt="image" src="https://github.com/user-attachments/assets/588b98cf-e273-460d-ba5a-b4e716b523dc" />


from typing import List

def printRowWise(a: List[List[int]]) -> List[int]:
    result = []
    
    for row in a:            # iterate row-wise
        for value in row:    # iterate column-wise
            result.append(value)
    
    return result
 or

 <img width="788" height="352" alt="image" src="https://github.com/user-attachments/assets/ba90cf19-834d-48cd-af89-828f88b5bcc2" />

## column wise traversal

<img width="949" height="454" alt="image" src="https://github.com/user-attachments/assets/e19dd699-bce1-4108-bb35-f49843ff0fee" />

## reshape matrix

covert dimension1 matrix to dim2 mtrix and reshape is only possible if #elemnts in dim1  is equal to #elements in dim2

<img width="433" height="242" alt="image" src="https://github.com/user-attachments/assets/eda0b072-d444-4770-a563-93148271a164" />

<img width="413" height="307" alt="image" src="https://github.com/user-attachments/assets/8215def8-8ce1-45e9-871f-42729a0287d0" />

Traverse row wise and shift element into second matrix

<img width="498" height="272" alt="image" src="https://github.com/user-attachments/assets/d6aa35ed-afc4-4f81-976d-d26dfd3a97a6" />

<img width="341" height="182" alt="image" src="https://github.com/user-attachments/assets/9d90b97c-cd70-475f-aea5-04f078666d0a" />

<img width="374" height="249" alt="image" src="https://github.com/user-attachments/assets/4e4e276d-0f35-482f-9440-0a25676355f0" />

<img width="512" height="248" alt="image" src="https://github.com/user-attachments/assets/4a304e7d-3c11-4726-8497-0a05ed919442" />


## row wise sum

<img width="954" height="422" alt="image" src="https://github.com/user-attachments/assets/40223216-7260-4266-b126-9d9567567ff6" />
