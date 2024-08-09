### Problem Statement
To organise and group movie data by a custom month-year format (e.g., "Sept2022") based on the date_added field. Each group should include all movies added in that specific month and year, and the output should be ordered chronologically by this custom format.



# Solution
In order to convert the response in the desired output, I have used mongoDB aggregation functionality in MongoDB Atlas.

In this tab, I have created different stages in the pipeline, each having its own functionality.

![](https://github.com/user-attachments/assets/782d78d5-36bd-40a1-89ff-e71d3811f3d7)

I have created 7 stages in the pipeline. Let’s understand the each stage one by one:-

Stage 1
-------------
Firstly, I want to filter out the values that may be null or empty string. So for that I have selected “$match” from the stage dropdown. It will exclude the data that has an empty string.

![](https://github.com/user-attachments/assets/dc3cda27-5c89-4187-8b20-f541d0b03992)

Stage 2
-------------
Then we will also filter the data that has null in date_added field. So for that I have again selected “$match” from the stage dropdown. It will exclude the data that has null as value for date_added field.

![](https://github.com/user-attachments/assets/cde3397b-bf9f-4096-95f6-68b072a6d228)

Stage 3
-------------
Now we will be adding a new field named, “date_added_trimmed”. It will contain a trimmed date string so that we can process the data efficiently. As previously I have seen date string that have unnecessary blank space. It will take date_added as input and will trim all the blank char " ".

So now the date_added_trimmed will have something like this : 


date_added_trimmed : "September 16, 2021"

This field is created from the date added field.


![](https://github.com/user-attachments/assets/7a4d3d6d-8f13-40a9-9646-3e67f069a4e4)

Stage 4
-------------
Now the date added trimmed is in string value, we would need to convert it into Date format to process it further. Hence, I have created a new field name “date_added_converted”. It will have date in Date format as per JS. It would be in format (%B %d, %Y). Here, B means month, d means date and Y means Year. 
The output would be like this 


![](https://github.com/user-attachments/assets/c6a9f1af-35f9-4368-97f4-1d39ff231445)

Stage 5
-------------
Since we are asked to group the item in this format "Sept2022". Hence, we would require a new field name “monthYear” to group it further as per the “monthYear” field.

Hence, I have created a new stage of addField in which monthYear is created. Now it will have the format “%b%Y”. Here b means month and Y means year. It will be in month year format (eg. Sept2022).


![](https://github.com/user-attachments/assets/c485eddf-9910-491e-9d22-fdbcc315b823)

Stage 6
-------------
Now we will finally group the data into the format that has been asked. So for that I have used “group” from stage dropdown.

It will have an id as “monthYear”, so that it can group documents by the monthYear field.

Then items have been created and using the “push”, it adds each document's fields into the items array for each group.


![](https://github.com/user-attachments/assets/63d6175c-d6ab-4ea4-9ce4-bf8682b523fd)

Stage 7
-------------
In addition to the required functionality, I have also sorted the response in the ascending order as per _id which is monthYear for us.

![](https://github.com/user-attachments/assets/6a3769cf-081c-437a-a53a-293c949d27b8)


Result Achieved :
-------------
We have grouped the data as per the monthYear format successfully.

![](https://github.com/user-attachments/assets/457eb14a-83be-4638-8ca0-f27c6fe27a45)
