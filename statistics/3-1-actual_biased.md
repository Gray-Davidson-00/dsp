#[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

#Exercise 3.1 Something like the class size paradox appears if you survey
#children and ask how many children are in their family. Families with many
#children are more likely to appear in your sample, and families with no children
#have no chance to be in the sample.

#Use the NSFG respondent variable NUMKDHH to construct the actual distribution
#for the number of children under 18 in the household.

#Now compute the biased distribution we would see if we surveyed the children
#and asked them how many children under 18 (including themselves) are in
#their household.

#Plot the actual and biased distributions, and compute their means. As a
#starting place, you can use chap03ex.ipynb.

import nsfg
import math
import thinkstats2
import pandas as pd
import thinkplot

#pd.set_option('display.max_colwidth', -1)
#pd.set_option('display.max_columns', None)  


df = nsfg.ReadFemPreg()
live = df[df.outcome == 1]

# prints full list of column names
#print(list(df.columns))


#numKids = df['numkdhh']
#print (numKids)




# code for the un-biased distribution
resp = nsfg.ReadFemResp()
pmf = thinkstats2.Pmf(resp.numkdhh, label='numkdhh')
print('UnBiased Mean: ', pmf.Mean())


# biased distribution
new_pmf = pmf
for x, p in pmf.Items():
	new_pmf.Mult(x, x)
new_pmf.Normalize()
print('Biased Mean: ', new_pmf.Mean())



# plot against each other
#biased_pmf = BiasPmf(pmf, label='observed')
thinkplot.PrePlot(2)
thinkplot.Pmfs([pmf, new_pmf])
thinkplot.Show(xlabel='family size', ylabel='PMF')
