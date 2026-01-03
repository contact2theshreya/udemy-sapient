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
