# Walmart TripTypes Dataset

Walmart has generated a list of trip types for which they want to classify all transactions. The trip types were generated
by Walmart data scientists over many years, but now Wal-mart would like a ML algorithm that will automatically classify
sales transactional data with trip types.

### Source

This data source originally came from a [Kaggle Competition](https://www.kaggle.com/c/walmart-recruiting-trip-type-classification).

### Transaction

Note that this is a transactional data.  Before running our analysis, we may want to perform a pivot or rollup of the
data to get all items fora given transation in a single row.

### Sample Transaction Data
| "TripType" | "VisitNumber" | "Weekday" | "Upc"       | "ScanCount" | "DepartmentDescription"    | "FinelineNumber" | 
|------------|---------------|-----------|-------------|-------------|----------------------------|------------------| 
| 999        | 5             | "Friday"  | 68113152929 | -1          | "FINANCIAL SERVICES"       | 1000             | 
| 30         | 7             | "Friday"  | 60538815980 | 1           | "SHOES"                    | 8931             | 
| 30         | 7             | "Friday"  | 7410811099  | 1           | "PERSONAL CARE"            | 4504             | 
| 26         | 8             | "Friday"  | 2238403510  | 2           | "PAINT AND ACCESSORIES"    | 3565             | 
| 26         | 8             | "Friday"  | 2006613744  | 2           | "PAINT AND ACCESSORIES"    | 1017             | 
| 26         | 8             | "Friday"  | 2006618783  | 2           | "PAINT AND ACCESSORIES"    | 1017             | 
| 26         | 8             | "Friday"  | 2006613743  | 1           | "PAINT AND ACCESSORIES"    | 1017             | 
| 26         | 8             | "Friday"  | 7004802737  | 1           | "PAINT AND ACCESSORIES"    | 2802             | 
| 26         | 8             | "Friday"  | 2238495318  | 1           | "PAINT AND ACCESSORIES"    | 4501             | 
| 26         | 8             | "Friday"  | 2238400200  | -1          | "PAINT AND ACCESSORIES"    | 3565             | 
| 26         | 8             | "Friday"  | 5200010239  | 1           | "DSD GROCERY"              | 4606             | 
| 26         | 8             | "Friday"  | 88679300501 | 2           | "PAINT AND ACCESSORIES"    | 3504             | 
| 26         | 8             | "Friday"  | 22006000000 | 1           | "MEAT - FRESH & FROZEN"    | 6009             | 
| 26         | 8             | "Friday"  | 2236760452  | 1           | "PAINT AND ACCESSORIES"    | 7                | 
| 26         | 8             | "Friday"  | 88679300501 | -1          | "PAINT AND ACCESSORIES"    | 3504             | 
| 26         | 8             | "Friday"  | 2238400200  | 2           | "PAINT AND ACCESSORIES"    | 3565             | 
| 26         | 8             | "Friday"  | 3019294203  | 1           | "PAINT AND ACCESSORIES"    | 2801             | 
| 26         | 8             | "Friday"  | 72450408840 | 1           | "PAINT AND ACCESSORIES"    | 1028             | 
| 26         | 8             | "Friday"  | 25541500000 | 2           | "DAIRY"                    | 1305             | 
| 26         | 8             | "Friday"  | 2310010776  | 1           | "PETS AND SUPPLIES"        | 3300             | 
| 26         | 8             | "Friday"  | 72450403700 | 2           | "PAINT AND ACCESSORIES"    | 1018             | 
| 26         | 8             | "Friday"  | 7874204967  | 1           | "HOUSEHOLD CHEMICALS/SUPP" | 707              | 
| 26         | 8             | "Friday"  | 5114139038  | 1           | "PAINT AND ACCESSORIES"    | 4415             | 
| 26         | 8             | "Friday"  | 5114197561  | 1           | "PAINT AND ACCESSORIES"    | 4415             | 
| 26         | 8             | "Friday"  | 3270011053  | 3           | "PETS AND SUPPLIES"        | 1001             | 
| 26         | 8             | "Friday"  |             | 1           | "NULL"                     |                  | 
| 8          | 9             | "Friday"  | 1070080727  | 1           | "IMPULSE MERCHANDISE"      | 115              | 
| 8          | 9             | "Friday"  | 3107        | 1           | "PRODUCE"                  | 103              | 


### Transformation

To save time, I have written a python script that pivots the data.  This is similar to a sql pivot.  

Here are the changes I have made:

1. Change day of the week into an integer field (can't vectorize a string.
2. Sum: Number of Items as NumItems
3. Return: Number of Items Returned
4. Pivoted Columns: Total number of items in each category

The end result is that every transaction is now on one row, rather than before, it is spread across multiple rows.


To run this, run the following:

```bash
  python triptype-transform.py

```


### Transformed data sample

| VisitNumber | TripType | Weekday | NumItems | Return | 1-HR PHOTO | ACCESSORIES | AUTOMOTIVE | BAKERY | BATH AND SHOWER | BEAUTY | BEDDING | BOOKS AND MAGAZINES | BOYS WEAR | BRAS & SHAPEWEAR | CAMERAS AND SUPPLIES | "CANDY, TOBACCO, COOKIES" | CELEBRATION | COMM BREAD | CONCEPT STORES | COOK AND DINE | DAIRY | DSD GROCERY | ELECTRONICS | FABRICS AND CRAFTS | FINANCIAL SERVICES | FROZEN FOODS | FURNITURE | "GIRLS WEAR, 4-6X  AND 7-14" | GROCERY DRY GOODS | HARDWARE | HEALTH AND BEAUTY AIDS | HOME DECOR | HOME MANAGEMENT | HORTICULTURE AND ACCESS | HOUSEHOLD CHEMICALS/SUPP | HOUSEHOLD PAPER GOODS | IMPULSE MERCHANDISE | INFANT APPAREL | INFANT CONSUMABLE HARDLINES | JEWELRY AND SUNGLASSES | LADIES SOCKS | LADIESWEAR | LARGE HOUSEHOLD GOODS | LAWN AND GARDEN | "LIQUOR,WINE,BEER" | MEAT - FRESH & FROZEN | MEDIA AND GAMING | MENSWEAR | OFFICE SUPPLIES | OPTICAL - FRAMES | OPTICAL - LENSES | OTHER DEPARTMENTS | PAINT AND ACCESSORIES | PERSONAL CARE | PETS AND SUPPLIES | PHARMACY OTC | PHARMACY RX | PLAYERS AND ELECTRONICS | PLUS AND MATERNITY | PRE PACKED DELI | PRODUCE | SEAFOOD | SEASONAL | SERVICE DELI | SHEER HOSIERY | SHOES | SLEEPWEAR/FOUNDATIONS | SPORTING GOODS | SWIMWEAR/OUTERWEAR | TOYS | WIRELESS | 
|-------------|----------|---------|----------|--------|------------|-------------|------------|--------|-----------------|--------|---------|---------------------|-----------|------------------|----------------------|---------------------------|-------------|------------|----------------|---------------|-------|-------------|-------------|--------------------|--------------------|--------------|-----------|------------------------------|-------------------|----------|------------------------|------------|-----------------|-------------------------|--------------------------|-----------------------|---------------------|----------------|-----------------------------|------------------------|--------------|------------|-----------------------|-----------------|--------------------|-----------------------|------------------|----------|-----------------|------------------|------------------|-------------------|-----------------------|---------------|-------------------|--------------|-------------|-------------------------|--------------------|-----------------|---------|---------|----------|--------------|---------------|-------|-----------------------|----------------|--------------------|------|----------| 
| 5           | 999      | 5       | -1       | 1.0    | 0.0        | 0.0         | 0.0        | 0.0    | 0.0             | 0.0    | 0.0     | 0.0                 | 0.0       | 0.0              | 0.0                  | 0.0                       | 0.0         | 0.0        | 0.0            | 0.0           | 0.0   | 0.0         | 0.0         | 0.0                | -1.0               | 0.0          | 0.0       | 0.0                          | 0.0               | 0.0      | 0.0                    | 0.0        | 0.0             | 0.0                     | 0.0                      | 0.0                   | 0.0                 | 0.0            | 0.0                         | 0.0                    | 0.0          | 0.0        | 0.0                   | 0.0             | 0.0                | 0.0                   | 0.0              | 0.0      | 0.0             | 0.0              | 0.0              | 0.0               | 0.0                   | 0.0           | 0.0               | 0.0          | 0.0         | 0.0                     | 0.0                | 0.0             | 0.0     | 0.0     | 0.0      | 0.0          | 0.0           | 0.0   | 0.0                   | 0.0            | 0.0                | 0.0  | 0.0      | 
| 7           | 30       | 5       | 2        | 0.0    | 0.0        | 0.0         | 0.0        | 0.0    | 0.0             | 0.0    | 0.0     | 0.0                 | 0.0       | 0.0              | 0.0                  | 0.0                       | 0.0         | 0.0        | 0.0            | 0.0           | 0.0   | 0.0         | 0.0         | 0.0                | 0.0                | 0.0          | 0.0       | 0.0                          | 0.0               | 0.0      | 0.0                    | 0.0        | 0.0             | 0.0                     | 0.0                      | 0.0                   | 0.0                 | 0.0            | 0.0                         | 0.0                    | 0.0          | 0.0        | 0.0                   | 0.0             | 0.0                | 0.0                   | 0.0              | 0.0      | 0.0             | 0.0              | 0.0              | 0.0               | 0.0                   | 1.0           | 0.0               | 0.0          | 0.0         | 0.0                     | 0.0                | 0.0             | 0.0     | 0.0     | 0.0      | 0.0          | 0.0           | 1.0   | 0.0                   | 0.0            | 0.0                | 0.0  | 0.0      | 
| 8           | 26       | 5       | 28       | 1.0    | 0.0        | 0.0         | 0.0        | 0.0    | 0.0             | 0.0    | 0.0     | 0.0                 | 0.0       | 0.0              | 0.0                  | 0.0                       | 0.0         | 0.0        | 0.0            | 0.0           | 2.0   | 1.0         | 0.0         | 0.0                | 0.0                | 0.0          | 0.0       | 0.0                          | 0.0               | 0.0      | 0.0                    | 0.0        | 0.0             | 0.0                     | 1.0                      | 0.0                   | 0.0                 | 0.0            | 0.0                         | 0.0                    | 0.0          | 0.0        | 0.0                   | 0.0             | 0.0                | 1.0                   | 0.0              | 0.0      | 0.0             | 0.0              | 0.0              | 0.0               | 18.0                  | 0.0           | 4.0               | 0.0          | 0.0         | 0.0                     | 0.0                | 0.0             | 0.0     | 0.0     | 0.0      | 0.0          | 0.0           | 0.0   | 0.0                   | 0.0            | 0.0                | 0.0  | 0.0      | 
| 9           | 8        | 5       | 3        | 0.0    | 0.0        | 0.0         | 0.0        | 0.0    | 0.0             | 0.0    | 0.0     | 0.0                 | 0.0       | 0.0              | 0.0                  | 0.0                       | 0.0         | 0.0        | 0.0            | 0.0           | 0.0   | 0.0         | 0.0         | 0.0                | 0.0                | 0.0          | 0.0       | 0.0                          | 0.0               | 0.0      | 0.0                    | 0.0        | 0.0             | 0.0                     | 0.0                      | 0.0                   | 1.0                 | 0.0            | 0.0                         | 0.0                    | 0.0          | 0.0        | 0.0                   | 0.0             | 0.0                | 0.0                   | 0.0              | 0.0      | 0.0             | 0.0              | 0.0              | 0.0               | 0.0                   | 0.0           | 0.0               | 0.0          | 0.0         | 0.0                     | 0.0                | 0.0             | 2.0     | 0.0     | 0.0      | 0.0          | 0.0           | 0.0   | 0.0                   | 0.0            | 0.0                | 0.0  | 0.0      | 
| 10          | 8        | 5       | 3        | 0.0    | 0.0        | 0.0         | 0.0        | 0.0    | 0.0             | 0.0    | 0.0     | 0.0                 | 0.0       | 0.0              | 0.0                  | 1.0                       | 0.0         | 0.0        | 0.0            | 0.0           | 0.0   | 2.0         | 0.0         | 0.0                | 0.0                | 0.0          | 0.0       | 0.0                          | 0.0               | 0.0      | 0.0                    | 0.0        | 0.0             | 0.0                     | 0.0                      | 0.0                   | 0.0                 | 0.0            | 0.0                         | 0.0                    | 0.0          | 0.0        | 0.0                   | 0.0             | 0.0                | 0.0                   | 0.0              | 0.0      | 0.0             | 0.0              | 0.0              | 0.0               | 0.0                   | 0.0           | 0.0               | 0.0          | 0.0         | 0.0                     | 0.0                | 0.0             | 0.0     | 0.0     | 0.0      | 0.0          | 0.0           | 0.0   | 0.0                   | 0.0            | 0.0                | 0.0  | 0.0      | 

### Predictions

We may want to use this to make a prediction.  In this case, the prediction variable will be "TripType".  Note that this
is in the training dataset but not the test dataset.




## Here is a List of the Trip TYpes and Description

Here's a brief description of the triptypes. Note that the Trip type somewhat corresponds to the department description,
but not completely.  Note that this is descriptive and not prescriptive.  In ML we are inductively trying to generate 
descriptions based on assigned triptype.  The description is for informational value only.

| TripTypeID | TripTypeDescription             | 
|------------|---------------------------------| 
| 3          | Financial Services              | 
| 4          | Pharmacy Runs                   | 
| 5          | Pharmacy Runs                   | 
| 6          | Booze and Calories              | 
| 7          | Strictly Grocery                | 
| 8          | Grocery and General Merchandise | 
| 9          | Mens Mixed Merchandise          | 
| 12         | Mixed Grocery and Household     | 
| 14         | Michaels Run                    | 
| 15         | Party Trip                      | 
| 18         | Toys                            | 
| 19         | Electronics                     | 
| 20         | Automotive                      | 
| 21         | Office and Crafts               | 
| 22         | Gaming and Media Electronics    | 
| 23         | Media Players                   | 
| 24         | Kitchen and Bath                | 
| 25         | Apparel Male Focused            | 
| 26         | Home Improvement Run            | 
| 27         | Lawn and Garden                 | 
| 28         | Sporting Goods                  | 
| 29         | Kids Sports                     | 
| 30         | Shoes and Jewelry               | 
| 31         | Cellphone                       | 
| 32         | Baby                            | 
| 33         | Cleaning Supplies               | 
| 34         | Pets                            | 
| 35         | Brand-name Grocery              | 
| 36         | Beauty and Personal Care        | 
| 37         | Produce Grocery                 | 
| 38         | Gallon of Milk                  | 
| 39         | Mixed Grocery                   | 
| 40         | Nonperishable Grocery           | 
| 41         | Return Trip                     | 
| 42         | Mixed Impulse                   | 
| 43         | Broad Mix                       | 
| 44         | Mixed Personal and Grocery      | 
| 999        | Other                           | 


