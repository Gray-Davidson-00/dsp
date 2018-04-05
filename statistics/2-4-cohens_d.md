#[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24)  (Cohen's d)





#Exercise 2.4 Using the variable totalwgt_lb, investigate whether first babies
#are lighter or heavier than others. Compute Cohen’s d to quantify the
#difference between the groups. How does it compare to the difference in
#pregnancy length?

import nsfg
import math


#df = nsfg.ReadFemPreg()

#print(df.columns)
#totalwgt_lb is the variable name for baby weight at birth
#print (df.totalwgt_lb )
# There are lots of NaNs in that data.  
# We're also going to need to separate it by first births (and maybe by living births)?


#print(df.head(10))

preg = nsfg.ReadFemPreg()
live = preg[preg.outcome == 1]


firsts = live[live.birthord == 1]
others = live[live.birthord != 1]

firstMean = firsts.totalwgt_lb.mean()
firstVar = firsts.totalwgt_lb.var()
firstStd = firsts.totalwgt_lb.std()

otherMean = others.totalwgt_lb.mean()
otherVar = others.totalwgt_lb.var()
otherStd = others.totalwgt_lb.std()


#print(firstMean,otherMean)

#https://stackoverflow.com/questions/22341271/get-list-from-pandas-dataframe-column
firstWeight = firsts['totalwgt_lb']
#.tolist()
otherWeight = others['totalwgt_lb'] 
#.tolist()

group1 = firstWeight
group2 = otherWeight

#statement of cohen's D from the textbook:
'''
def CohenEffectSize(group1, group2):
	diff = group1.mean() - group2.mean()
	var1 = group1.var()
	var2 = group2.var()
	n1, n2 = len(group1), len(group2)
	pooled_var = (n1 * var1 + n2 * var2) / (n1 + n2)
	d = diff / math.sqrt(pooled_var)
	return d
'''

diff = firstWeight.mean() - otherWeight.mean()
var1 = firstWeight.var()
var2 = otherWeight.var()
n1, n2 = len(firstWeight), len(otherWeight)
pooled_var = (n1 * var1 + n2 * var2) / (n1 + n2)
d = diff / math.sqrt(pooled_var)



#Cohen_Weight = CohenEffectSize(firstWeight,otherWeight)

# and we make it very...obnoxiously clear what's going on:
print("Firsts Weight Mean: ", str.format('{0:.15f}', firstWeight.mean())) 
print("Others Weight Mean: ", str.format('{0:.15f}', otherWeight.mean()))
print ("diff", diff) 
print("First Weight Variance: ", str.format('{0:.15f}', firstWeight.var())) 
print("Others Weight Variance: ", str.format('{0:.15f}', otherWeight.var())) 
print ("Length of firsts", n1)
print ("Length of others", n2)
print ("pooled_var: ",pooled_var)
print ("sqrt of pooled_var: ", math.sqrt(pooled_var))
print ("cohen D: ", d)
print("cohen D: ", str.format('{0:.15f}', d)) 
#did this so there would be many significant digits but there is still no value.  

#print(firstWeight, otherWeight)





#Pregnancy length differed by about 0.2% between first and subsequent pregnancies (with first pregnancies being longer)
#birth-weight differs by 7.325855614973262-7.201094430437772/7.325855614973262 = .01703 = 1.703% with first pregnancies being lighter.  
# Cohen's D is -0.0886729 which I'm not really sure how to interpret.

#I find that: "Cohen suggested that d=0.2 be considered a 'small' effect size, 0.5 represents a 'medium' effect size and 0.8 a 'large' effect size. This means that if two groups' means don't differ by 0.2 standard deviations or more, the difference is trivial, even if it is statistically signficant."

#so I guess we'd say that this difference (-.09) is significant but unimportant.





