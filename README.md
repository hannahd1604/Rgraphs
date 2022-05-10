# Rgraphs
Rgraphs with ggplot


#AMOUNT OF CLONES setwd("\~/Documents/experiments/Heat shock") #does not make sense as repository is wd
install.packages("readxl") library(readxl)

dat \<- read_excel(file.choose())

#directly pick up file: dat \<-
read_excel('/Users/hd475/Documents/experiments/Heat shock/NB
counting.xlsx') View(dat)

install.packages("ggplot2") install.packages("dplyr") library(ggplot2)
library(tidyverse) library(ggpubr) library(rstatix) library(dplyr)

#change order and remove NA(use short version of table for this): dat =
na.omit(dat) HSrelevel \<- fct_relevel(dat\$HS, 'none', '1 min', '5
min', '10 min', '20 min', '30 min', '20-60-20', '45 min', '60 min', '90
min', '60-30-60', '120 min', '180 min')

#automatic colors

install.packages("RColorBrewer")

# BOXPLOT

#final graph ggplot(dat, aes(y=Ratio, x=HSrelevel, group=HSrelevel,
fill=HSrelevel))+theme_classic()+theme(legend.position="none")+
  theme(axis.title.y = element_text(size = 12, face=2))+theme(axis.title.x
                                                              = element_text(size = 12, face=2))+ scale_fill_brewer(palette='Set3')+
  labs(y="Ratio Clones (%)", x="Heat shock
(min)")+geom_boxplot()+geom_jitter()+theme(axis.text.x =
                                             element_text(angle = 90, vjust = 0.5, hjust=1))

#add stats

#only works with less comparisons (depending on the amount of data)
my_comparisons3 \<- list(c('none', '45 min'), c('none', '60 min'),
                         c('none', '90 min'))

ggplot(dat, aes(y=Ratio, x=HSrelevel, group=HSrelevel,
                fill=HSrelevel))+theme_classic()+theme(legend.position="none")+
  theme(axis.title.y = element_text(size = 12, face=2))+theme(axis.title.x
                                                              = element_text(size = 12, face=2))+ scale_fill_brewer(palette='Set3')+
  labs(y="Ratio Clones (%)", x="Heat shock
(min)")+geom_boxplot()+geom_jitter()+theme(axis.text.x =
                                             element_text(angle = 90, vjust = 0.5,
                                                          hjust=1))+stat_compare_means(comparison=my_comparisons3,
                                                                                       method="t.test", aes(label = ..p.signif..))DOT PLOT with colors by group
as dots

#ratio dpn RFP

ggplot(dat, aes(y=deadpan, x=clones, color=HSrelevel)) +
  geom_point(size=2)+ theme_classic()+ theme(axis.title.y =
                                               element_text(size = 12, face=2))+theme(axis.title.x = element_text(size
                                                                                                                  = 12, face=2))+ ylim(0,150)+ labs(y="# Deadpan-labelled cells", x="#
RFP-labelled cells")+scale_colour_discrete("Heat shock")
