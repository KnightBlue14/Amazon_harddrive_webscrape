# Amazon Webscraping
A personal project to compare the prices of hard drives from different manufacturers. As it is, the script takes information from the Amazon webpage and exports it to separate .csv files, though it can easily be adapted for different outputs, such as a database
## Description
The initial plan was to compare prices across multiple websites, such as ebay and newegg, though issues emerged, such as the webpages being inconsistent with the placement of elements or the sites using anti-scraping protection. In light of this, I opted to just use Amazon, since it would provide the products I wanted without blocking the request. The final version collects the prices of the top-rated hard drives and SSD's from Seagate, Western Digital, Samsung, Sandisk and Crucial, then outputs the results to individual .csv files. All in all, a relatively simple project once you know what you're doing

## Technologies used
* Python - Python was used to complete the entire project in it's current state. You could change it to include other tools, such as a SQL database for persistent storage, but that is beyond the focus of this script. If you are unsure where to begin, I have other projects that feature databases, so I would suggest starting with those.
## How to use

### Amazon_webscrape.ipynb

This is the only file needed for the project, covering the entire process of searching, scraping and exporting. 
* URL_{company} - These 5 variables are used to store the initial webpages, sorted by top-rated and filtered for each brand. For whatever project you aim to carry out, be it fewer or more brands, different sorting orders or different products altogether, this is where to start. 
* Webpage_{company},  soup_{company} and links_{company} - all of these variables follow on from the URL variables, so any adjustments you make there will need to be reflected here. The link selection should still work fine, you just need to change the name.
### The rest
This is where the bulk of your changes will need to be made depending on your needs. It has it's own section, so I can go over it bit by bit
* Links_set and df_name - Just change these to reflect your earlier changes - change the names, and add more if you're comparing more brands
* column_list - Adjust this depending on what variables you want to track. In this case, teh dataframe created will include the name, price, rating, number of reviews, drive capacity and the link to the product page.
The block dealing with the individual link can be left alone - I found that links collected from the webpage were inconsistent, sometimes including the amazon domain name, and sometimes not. This block simply removes it if it is present, then adds it in either way.
*  Try block - this will be the section that needs the most work when changing. It collects the information by targeting html elements. The first four are fine, as the elements are present on all pages. However, the capacity variable is specific to this project. As the placement of the capacity in technical information is inconsistent between products, I was unable to target an element for scraping. Instead, I check the title, which includes the capacity for that page, cut out that section of the title, then remove whitespace to leave just the capacity, in either TB or GB. If this were part of a larger project, I would format this to just TB. Finally, the entry variable will, again, need to be changed depending on what you want to track.
* For the final block, the replace function can be left alone. I noticed when testing that these three repeated at times, and upon investigation I found that some pages didn't have prices listed where they should be. They were available to buy, just hidden behind 'See all buying options'. An example of this is included in this repo. When this happened, variables from the previous page would be used instead, resulting in repeating values. This function removes these cases from the final dataframe. There will still be cases of review scores and numbers repeating, but this is because of the same product having different capacity options
* The output can be left alone or changed depending on what you want. If you want to use a database, you will need to set this up yourself, and edit the script accordingly. Alternatively, you can leave it as is, and set up a separate script to read the output files.
