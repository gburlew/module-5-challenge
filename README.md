# module-5-challenge

Here, I have organized the help I got by the resources I used during this project. I used tutoring sessions, AskBCS learning assistant, Xpert AI learning assistant, and the link that was provided within the original starter code to create a graph with multiple box plots.


## Xpert:
Added r in front of file paths so that jupyter notebook wouldn't interpret file paths incorrectly.
My code for the first bar chart accidentally used matplotlib while plotting, so xpert helped me correct it so that the code read:count.plot(kind="bar", xlabel="Drug Regimen", rot=90, ylabel="# of Observed Mouse Timepoints")
distpd.plot.pie(y='sizes', autopct='%1.1f%%', ylabel = "Sex"); this was to help me display the percentages of each pie slice. I had originally coded it as: distpd.plot(kind = "pie") plt.ylabel("Sex") before going to get help as I suspected that I was still using matplotlib instead of just pandas.
Xpert corrected my code from: 
plt.pie(distpd.values())
to: plt.pie(distpd.values, labels=distpd.index, autopct='%1.1f%%')

I was having trouble trying to filter the dataset so that it would only show rows where "timepoint_x" and "timepoint_y" had values that were equal to each other. Xpert corrected my original code from: tumor_vol_merge = tumor_vol_merge["Timepoint_x" == "Timepoint_y"]
to: 
tumor_vol_merge = tumor_vol_merge[tumor_vol_merge["Timepoint_x"] == tumor_vol_merge["Timepoint_y"]]

Corrected my code from:
  tumor_vol_merge.loc[(tumor_vol_merge["Drug Regimen"] == treatment)].median
    tumor_vol_merge.loc
to:
tumor_volumes = tumor_vol_merge.loc[tumor_vol_merge["Drug Regimen"] == treatment, "Tumor Volume (mm3")]
    tumor_vol_data.append(tumor_volumes)

ax.set_xticklabels(treatments)
^ When I asked how I could have each box plot named after the respective drug that they were measuring.

import warnings

with warnings.catch_warnings():
    warnings.simplefilter("ignore")
    single_mouse["Average Tumor Volume (mm3)"] = single_mouse.groupby("Mouse ID")["Tumor Volume (mm3)"].transform("mean")

with warnings.catch_warnings():
    warnings.simplefilter("ignore")
    average_tumor_volume = single_mouse.groupby('Mouse ID')['Tumor Volume (mm3)'].transform('mean')

with warnings.catch_warnings():
    warnings.simplefilter("ignore")
    single_mouse['Average Tumor Volume (mm3)'] = average_tumor_volume

single_mouse

correlation_coefficient, _ = st.pearsonr(single_mouse['Weight (g)'], single_mouse['Average Tumor Volume (mm3)'])

#Perform linear regression
slope, intercept, _, _, _ = st.linregress(single_mouse['Weight (g)'], single_mouse['Average Tumor Volume (mm3)'])

#Add the regression line to the scatter plot
plt.scatter(single_mouse['Weight (g)'], single_mouse['Average Tumor Volume (mm3)'])
plt.plot(single_mouse['Weight (g)'], slope * single_mouse['Weight (g)'] + intercept, color='red')

#Add correlation coefficient to the plot
print(f"The correlation between mouse weight and the average tumor volume is", correlation_coefficient)

## Tutoring:
I got help with coding from the start of "Summary Statistics" until the second bar chart, along with editing my original data merge code from:
mouse_data_merge = pd.merge(mouse_metadata, study_results how="left", on=["Mouse ID", "Mouse ID"]) 
to: 
mouse_data_merge = pd.merge(study_results, mouse_metadata, how="left", on=["Mouse ID"])

# AskBCS:
for x in treatments:
     dataframe_name.loc[etc.....

Corrected my code from: 
#Put treatments into a list for for loop (and later for plot labels)
treatments = ["Capomulin", "Ramicane", "Infubinol", "Ceftamin"]
#Create empty list to fill with tumor vol data (for plotting)
tumor_vol_data = []
#Calculate the IQR and quantitatively determine if there are any potential outliers.
for treatment in treatments:
    tumor_volumes = tumor_vol_merge.loc[tumor_vol_merge["Drug Regimen"] == treatment, "Tumor Volume (mm3)"]
    #add subset
    tumor_vol_data.append(tumor_volumes)
    #Locate the rows which contain mice on each drug and get the tumor volumes
tumor_volumes = tumor_vol_merge.loc[tumor_vol_merge["Drug Regimen"] == treatment, "Tumor Volume (mm3)"]
quartiles = tumor_volumes.quantile([.25, .75])
lowerq = quartiles[0.25]
upperq = quartiles[0.75]
iqr = upperq - lowerq
lower_bound = lowerq - (1.5 * iqr)
upper_bound = upperq + (1.5 * iqr)
    #Determine potential outliers
outliers = tumor_volumes.loc[(tumor_volumes < lower_bound) | (tumor_volumes > upper_bound)]
    #Print the results
print(f"Potential outliers for {treatment}: {outliers}")
#Print the tumor_vol_data list containing tumor volumes for each treatment
print(tumor_vol_data)
    #Determine outliers using upper and lower bounds
^ A large amount of thise code comes from attempting to receive ai assistance before using AskBCS.

to:
#Put treatments into a list for for loop (and later for plot labels)
treatments = ["Capomulin", "Ramicane", "Infubinol", "Ceftamin"]
#Create empty list to fill with tumor vol data (for plotting)
tumor_vol_data = []
#Calculate the IQR and quantitatively determine if there are any potential outliers.
for treatment in treatments:
#Locate the rows which contain mice on each drug and get the tumor volumes
tumor_volumes = tumor_vol_merge.loc[tumor_vol_merge["Drug Regimen"] == treatment, "Tumor Volume (mm3)"]
    # add subset
    tumor_vol_data.append(tumor_volumes)
#Determine outliers using upper and lower bounds
quartiles = tumor_volumes.quantile([.25, .75])
lowerq = quartiles[0.25]
upperq = quartiles[0.75]
iqr = upperq - lowerq
lower_bound = lowerq - (1.5 * iqr)
upper_bound = upperq + (1.5 * iqr)
    #Determine potential outliers
outliers = tumor_volumes.loc[(tumor_volumes < lower_bound) | (tumor_volumes > upper_bound)]
    #Print the results
print(f"Potential outliers for {treatment}: {outliers}")
#Print the tumor_vol_data list containing tumor volumes for each treatment
print(tumor_vol_data)
    #Determine outliers using upper and lower bounds

After receiving said tutoring help, I indented the code properly and got rid of the function that printed just the tumor volume data.

## Other:
I found the code: 
fig, ax = plt.subplots()
ax.boxplot(tumor_vol_data)
from the provided link in the module 5 challenge instructions where it mentioned that we are supposed to have every box plot in a single graph.
