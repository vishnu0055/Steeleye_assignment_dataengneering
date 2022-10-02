# XML Parser (Steeleye Assignment)

- This is an XML Parser code which parses a specific type of XML given in the assignment.

## Pipeline:
- The pipeline follows the following steps:<br>
(For steps 1 - 4 refer `main.ipynb`, for step 5 refer `s3.ipynb`):
  1. Downloading the XML from the [link](https://registers.esma.europa.eu/solr/esma_registers_firds_files/select?q=*&fq=publication_date:%5B2021-01-17T00:00:00Z+TO+2021-01-19T23:59:59Z%5D&wt=xml&indent=true&start=0&rows=100). <br>
  Functions `get_xml_file()` and `get_data_file()` handle the steps 1 - 3. <br>
  `get_data_file()` GETs the contents of the XML file given in the above link and creates a parse tree object into the file called ` data.xml `.<br>
  2. Parsing the first download link and downloading the zip file. <br>
  `get_xml_file()` parses for the first download link and downloads the zip file.
  3. Extracting the XML from the zip file.<br>
  `get_xml_file()` also extracts the downloaded zip file into the destination folder `data/`.
  4. Converting the contents of the XML into a CSV format. <br>
    Functions:<br>
      - ` get_file_size_in_mb(filepath) `: takes the filepath as its parameter and returns the size of the file.
      - ` get_xml_info(filepath) `: takes the filepath as its parameter and logs information like size of the file, total number of tags present in the file and total no. of unique tags.
      - ` clean_xml_file(doc) `: takes an etree object as its parameter, it cleans noisy tags <br>
      ex. ` <{urn:iso:std:iso:20022:tech:xsd:head.003.001.01}Pyld> ` to ` <Pyld> ` and writes changes to a new file called ` output.xml `. It returns a etree object of the cleaned file.
      - ` extract_data(root) `: takes the root etree element as its parameter, It parses for the required tags, creates a dataframe out of the extracted data and stores it into a csv file called ` dataset.csv `.
  
  
  5. Store the CSV file generated into an AWS S3 Bucket. <br>
  ` s3.ipynb ` contains the driver code for uploading the ` dataset.csv ` file onto the AWS S3 bucket named ` rohitest1 `. The hosted link is [https://vishnu0055.s3.us-east-2.amazonaws.com/datasheet.csv](https://vishnu0055.s3.us-east-2.amazonaws.com/datasheet.csv)

- Pydoc for each function is included in the code. Logging has been done to DEBUG and log the progress of the code and is stored in ` logs.log ` file.

## Unit Testing:
The ` test/ ` folder contains three unit test cases: 
 1. **Unit Test 1**: Testing done for the retrieval of parent XML file and extraction of the zip file from the given url (refer ` unit_test_1.ipynb `)
 2. **Unit Test 2**: Testing done for parsing and cleaning the extracted XML file (ie) simplifying tag names (refer ` unit_test_2.ipynb `)
 3. **Unit Test 3**: Testing done for parsing of required tags and attributes from the XML file and converting it into a CSV format. (refer ` unit_test_3.ipynb `)



*Thankyou for the opportunity, I thoroughly enjoyed and learned new strategies while doing the assignment. The data folder (which contains the XML files) has not been uploaded due to github's file size issues, but have been uploaded in internshala, zipped with the other files.*
