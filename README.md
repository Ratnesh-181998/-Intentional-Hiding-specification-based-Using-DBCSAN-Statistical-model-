Intentional Hiding:

![IH1](https://github.com/user-attachments/assets/81314031-21a7-49ec-bfc6-721ab80ed8ae)

Business Requirement: 

The GeM marketplace aims to ensure that all products listed are easily discoverable by buyers. However, 
sellers may attempt to hide certain products intentionally, either within the same or different 
categories, by providing unique or incorrect specifications.  
This requirement focuses on detecting such intentionally hidden products to ensure transparency and 
enhance the quality of listings.

Proposed solution: 

The proposed solution aims to identify hidden product catalogs by analyzing product specifications 
within categories, flagging entries with unique or incorrect attributes, and exporting the results for 
marketplace administrators to review.  
This will ensure that hidden products can be detected and corrected, improving searchability and 
reducing potential misuse of the system. 

Solution Consumption: 

The proposed solution can be effectively consumed by two key stakeholders: 
• Seller: Sellers will be restricted during the catalog upload process in CMS. The system will 
automatically check the product specifications entered by sellers, and if they match any criteria 
of hidden or incorrect specifications (e.g., unique or uncommon attributes), the upload will 
either be flagged or restricted. 
• GeM SPV: GeM SPV can utilize the flagged product data to perform market sanitization by 
reviewing products with rare or suspicious specifications. The solution allows GeM 
administrators to proactively monitor and take action on these flagged products. 



Data: 

The required data can be fetched from below tables to identify intentionally hidden product catalogs in 
the GeM marketplace: 
• Table: inb_variants  
• Table: inb_catalog_attrs


![Approch](https://github.com/user-attachments/assets/0bad5e7e-49e4-4daa-ab7f-8e5f6be72e1f)


Steps In Model:  

1. Data Extraction: 
• Source: Product information will be extracted from the GeM staging database using SQL queries. 
This includes product ID, category information, catalog ID, and technical parameters. 
• Target: The focus will be on active products within specified categories. 
2. Technical Parameter Cleaning: 
The raw product technical parameters often contain unnecessary lines (e.g., weights) and formatting 
issues. These will be cleaned using a Python function to remove irrelevant data and standardize the 
parameters for further analysis. 
3. Mapping Specifications to Categories: 
Using a predefined category specification mapping file, the technical parameters will be mapped to 
human-readable names for each category. This step ensures that all product attributes can be easily 
interpreted and compared. 
4. Concatenation of Product Specifications: 
All relevant technical parameters for a product will be concatenated into a single string. This allows 
for easy identification of unique or rare combinations of specifications that might indicate hidden 
products.
5. Frequency Analysis of Specifications: 
Once specifications are concatenated, the frequency of each unique combination will be analyzed 
within the same category. Products with specifications that occur less than a certain threshold (e.g., 
three or more occurrences) will be flagged as potentially hidden or incorrectly categorized. 
6. Flagging Hidden Products: 
Products with low-frequency specification combinations will be flagged for further review. These 
flagged products may be intentionally hidden or the result of data entry mistakes. 
7. Data Export: 
The final dataset, containing product details, concatenated specifications, frequency counts, and flag 
indicators, will be exported to a CSV file. This file will allow GeM to review and take action on 
potentially hidden or miscategorized products.

![Flow Diagram](https://github.com/user-attachments/assets/0867810a-135b-4edc-86d4-6116f19d370c)


Business Value: 

1. Transparency: Ensures that sellers cannot hide products in the marketplace by using incorrect or 
unique specifications. 
2. Error Correction: Identifies and corrects unintentional errors due to misinformed sellers. 
3. Improved Searchability: Helps users find relevant products more efficiently by minimizing hidden or 
misplaced product listings. 
4. Enhanced Monitoring: Provides marketplace administrators with a tool to monitor and review 
flagged product listings for policy violations or errors.

