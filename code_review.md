# Code Review: Project 2

### Name: Michael Green 

[X] README.md included
[X] Slides included
[X] Code included

## Clean Code:
- Great use of separate scraping module with mymovie.py! Even better that its OOP 
- You can remove all the notes to yourself at the beginning about the challenege set, etc. to make the final version more clean. 
- You can delete any commented out/unused/unrun cells and sections; and 'notes' to self about what needs to be done still throughout
- Good command of Pandas 

## Good Documentation: 
- Excellent readme.md! Love the embedded images and links for clarity and style, and the explanations of each notebook. I'm also impressed by the 'steps to produce this project' section -- very useful! 
- I'd love to see a results section in the readme -- just a high level summary of your conclusions and takeaways from doing this project 
- I like that you included an image of the html, gives the reader context about the scraping.
- Good explanation of your model selection -- I'd love to see additional citation in this section of what scores etc. led you to choose it/think it was overfit. 

## Proper Data Science: 
- Clear question of predicting star rating specifically on opening day 
- I'm impressed with the mymovie.py function -- both object oriented and extensive! 
- Great job first doing EDA, to get an in-depth understanding of your data and which features are actually linearly related hence which to include. 
- Nice work trying IQR to remove outliers, and explaining the rationale behind actually keeping them.  
- In the future, heat maps can be used with correlation matrixes to make them more visually approachable. Yours is a bit hard at a glance to draw info out of. 
- It was a great idea engineering a "star power" feature to represent directors/actors! Since you're right, one-hot encoding all names would not be feasible or probably meaningful 
- Nice visualizations of positive and negative influencing features on separate charts -- it would be great to include a markdown cell with some analysis of these 
- Great residuals and Q-Q plots!! And they indicate a well-functioning model :) 

## Comments: 
- Great job on project 2! 
- Very thoughtful feature engineering
- I'd just love to see a conclusions section with your analysis of the meaning & takeaway of your project, and cleaning up of the commented out sections -- its unclear as is whether you used them or not
