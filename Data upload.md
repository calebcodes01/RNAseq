## Uploading DESeq2 data to R

This package takes in DESeq2 output. To upload an excel file as a usable dataframe install the following package

	install.packages("readxl")

Load the package

	library ("readxl")

Usage for the first sheet in an .xls file

	df <- read_excel("~/path/to/file.xls")
  
Usage if you wish to reference a specific sheet

	df <- read_excel("~/path/to/file.xls", sheet = 2)
  
