## Problem
    
    Given a spark dataframe with multiple columns containing IPv4 address,
    
    Your task is to return the columns where all the values in these columns are correctly formatted. 
    The correct formats are: y.y.y.y, y-y-y-y and y:y:y:y" (0<=y<=255) and nothing else.
    
### Assumptions
 
    1) No need to validate contents (that means 0.0.0.0 and 255.255.255.255 are all valid values).
    
    2) Null value does not represent correct format
    
### Examples
    
    Input:

| Column 1  | Column 2 | Column 3  | Column 4 | Column 5 |
| :---: | :---: | :---: |  :---: | :---: |
| 11.22.33.44  | 11-22-33-44 | 11.22.33.44 | 11-22-33-44 | 11.22.33.44 |
| 55.66.77.88  | 55-66-77-88 | 55.66.77  | 55-66-777-88 | Null |
| 99.00.11.22  | 99-00-11-22 | 88-99-00-11  | 99-00-11-22 | Null |

    Output:
    
| Column 1  | Column 2 |  
| :---: | :---: |  
| 11.22.33.44  | 11-22-33-44 |  
| 55.66.77.88  | 55-66-77-88 |  
| 99.00.11.22  | 99-00-11-22 |    
      