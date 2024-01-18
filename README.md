# AWS-Lab-Composite-Data-Types

Creating a car inventory data
Comma-separated values (CSV) is a file format that’s used to store tabular data, such as data from a spreadsheet. You will work with the CSV file from the following block.

From the menu bar, choose File New File.
This action creates an untitled file.

Choose File Save As…, and save the file as 

car_fleet.csv

Copy and paste the following text block into the car_fleet.csv file and save the file.


vin,make,model,year,range,topSpeed,zeroSixty,mileage
TMX20122,AnyCompany Motors, Coupe, 2012, 335, 155, 4.1, 50000
TM320163,AnyCompany Motors, Sedan, 2016, 240, 140, 5.2, 20000
TMX20121,AnyCompany Motors, SUV, 2012, 295, 155, 4.7, 100000
TMX20204,AnyCompany Motors, Truck, 2020, 300, 155, 3.5, 0
Tip: If a pop-up window opens with the message Native Clipboard Unavailable, use the keyboard, not the browser menu, to perform copy and paste actions. For example, on Windows, use CTRL+C and CTRL+V to copy and paste, respectively. On Mac, use Command+C and Command+V.

Creating a car inventory program
Defining the dictionary
You will read in the file by using a module called 

csv
. Additionally, you will make a deep copy of the data to store in memory by using a module called 

copy
.

From the navigation pane of the IDE, choose (double-click) the .py file that you created in the previous Creating your Python exercise file section.

First, import the modules that you will use:


import csv
import copy
Next, define a dictionary that will serve as your composite type for reading the tabular data:

myVehicle = {
        "vin" : "<empty>",
        "make" : "<empty>" ,
        "model" : "<empty>" ,
        "year" : 0,
        "range" : 0,
        "topSpeed" : 0,
        "zeroSixty" : 0.0,
        "mileage" : 0
    }
You will use a 

for
 loop to iterate over the initial keys and values of the dictionary.

for key, value in myVehicle.items():
print("{} : {}".format(key,value))
Note: The items() function belongs to the dictionary data type. The items() function tells the 

for
 loop to traverse the collection owned by the dictionary data type.

Define an empty list to hold the car inventory that you will read:

myInventoryList = []
Save the file.
Copying the CSV file into memory
You will read in the data from disk (hard drive) and make an in-memory (random access memory, or RAM) copy. In a computer, a hard drive stores data long term, including when the power is turned off. RAM refers to temporary memory that is faster, but it is erased when the computer’s power is turned off.

You will be introduced to the 

with open
 syntax statement, which keeps a file open while you read data. It will automatically close the CSV file when the code inside the 

with
 block is finished running.

You will also use a new way of formatting a string. Instead of using double quotation marks and .format to pass in the variables, you can use a single quotation mark and write in the variables between the “{}” symbols.

Finally, csv.reader() is a function that you are using from the 

csv
 library that you imported with the 

import csv
 statement.

Most of the rest of the code should be familiar.

Now, return to the Python file:

Enter the following code:

with open('car_fleet.csv') as csvFile:
	csvReader = csv.reader(csvFile, delimiter=',')  
	lineCount = 0  
	for row in csvReader:
		if lineCount == 0:
			print(f'Column names are: {", ".join(row)}')  
			lineCount += 1  
		else:  
			print(f'vin: {row[0]} make: {row[1]}, model: {row[2]}, year: {row[3]}, range: {row[4]}, topSpeed: {row[5]}, zeroSixty: {row[6]}, mileage: {row[7]}')  
			currentVehicle = copy.deepcopy(myVehicle)  
			currentVehicle["vin"] = row[0]  
			currentVehicle["make"] = row[1]  
			currentVehicle["model"] = row[2]  
			currentVehicle["year"] = row[3]  
			currentVehicle["range"] = row[4]  
			currentVehicle["topSpeed"] = row[5]  
			currentVehicle["zeroSixty"] = row[6]  
			currentVehicle["mileage"] = row[7]  
			myInventoryList.append(currentVehicle)  
			lineCount += 1  
	print(f'Processed {lineCount} lines.')
Though this code seems like a large amount of code to process, it mostly comprises statements that you saw in earlier labs. You have a 

for
 loop with an 

if-else
 statement followed by a 

print()
 statement at the end.

However, the following line needs further explanation:


currentVehicle = copy.deepcopy(myVehicle)
By default, Python does a shallow copy of complex data types. A shallow copy refers, or points, to the storage location of the myVehicle dictionary variable. Without this line, you would have only one storage box, and only the last item in the list would be copied into memory. This line makes sure that new storage boxes are created in memory to store the new tabular data that is being read.

Printing the car inventory
You will finish the Python script by printing the car inventory from the myInventoryList variable.

Return to the Python script, and enter the following code:

for myCarProperties in myInventoryList:
for key, value in myCarProperties.items():
print("{} : {}".format(key,value))
print("-----")
Save the file.

Choose the Run button in the menu bar to run the program.

Confirm that the script runs correctly and that the output displays as you expect it to.

Review the code for reading in the tabular data from the CSV file one more time. Understanding this section of the code is key to this lab.

From the navigation pane of the IDE, you may choose to download the file and save it on your local desktop for future reference.

Conclusion
 Congratulations! You now have successfully done the following:

Used numeric data types

Used string data types

Used the dictionary data type

Used the list data type

Used a for loop

Used the print() function

Used the if statement

Used the else statement

Used the import statement
