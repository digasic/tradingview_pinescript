Study - Probability Zones


![image probability zones](https://i.imgur.com/TNSJjfs.png)

Warns aswell about areas where a possible extreme movement could appear

![image probability zones2](https://i.imgur.com/2BM7HTo.png)

```

//@version=2
study("Probability Zones",overlay=true)
p=2
sm=15
b=3
w=3
c=close
t=10
numbands=5
breakout1=1.035//1.115
breakout2=1.025//1.104
filteroutbreakouts=0.011//0.035

lc=linreg(c,sm,0)

Z1=w*stdev(c,p*(1+b*0))
Z2=w*stdev(c,p*(1+b*1))
Z3=w*stdev(c,p*(1+b*2))
Z4=w*stdev(c,p*(1+b*3))
Z5=w*stdev(c,p*(1+b*4))

a1=plot(numbands>0?lc+Z1:c,color=white,style=line,transp=100)
a2=plot(numbands>0?lc-Z1:c,color=white,style=line,transp=100)

b1=plot(numbands>1?lc+Z2:c,color=white,style=line,transp=100)
b2=plot(numbands>1?lc-Z2:c,color=white,style=line,transp=100)

c1=plot(numbands>2?lc+Z3:c,color=white,style=line,transp=100)
c2=plot(numbands>2?lc-Z3:c,color=white,style=line,transp=100)

d1=plot(numbands>3?lc+Z4:c,color=white,style=line,transp=100)
d2=plot(numbands>3?lc-Z4:c,color=white,style=line,transp=100)

e1=plot(numbands>4?lc+Z5:c,color=white,style=line,transp=100)
e2=plot(numbands>4?lc-Z5:c,color=white,style=line,transp=100)

fill(a1,e1,color=white,transp=numbands>0?100-1*t:100)
fill(a2,e2,color=white,transp=numbands>0?100-1*t:100)

fill(b1,e1,color=white,transp=numbands>1?100-1.5*t:100)
fill(b2,e2,color=white,transp=numbands>1?100-1.5*t:100)

fill(c1,e1,color=white,transp=numbands>2?100-2*t:100)
fill(c2,e2,color=white,transp=numbands>2?100-2*t:100)

fill(d1,e1,color=white,transp=numbands>3?100-2.5*t:100)
fill(d2,e2,color=white,transp=numbands>3?100-2.5*t:100)



diffx(a,b)=>(a-b)/((a+b)/2)


distC=(lc+Z3)/(lc-Z3)
distD=(lc+Z4)/(lc-Z4)
distE=(lc+Z5)/(lc-Z5)

distT=(distD+distE)/2

FilterOutBreakO=abs(diffx(distT,linreg(distT,50,0)))<filteroutbreakouts?1:0

y1=plot(distT<breakout1 and FilterOutBreakO==0?c*(1+distT/50):c,color=yellow,style=line,transp=100)
y2=plot(distT<breakout1 and FilterOutBreakO==0?c*(1-distT/50):c,color=yellow,style=line,transp=100)

fill(y1,y2,color=yellow,transp=70)

z1=plot(distT<breakout2 and FilterOutBreakO==0?c*(1+distT/50):c,color=red,style=line,transp=100)
z2=plot(distT<breakout2 and FilterOutBreakO==0?c*(1-distT/50):c,color=red,style=line,transp=100)

fill(z1,z2,color=red,transp=65)


AnchoHighest=200

ret=2


peak=Z4[ret]+lc[ret]>=highest(Z4[ret]+lc[ret],AnchoHighest) and Z4+lc<highest(Z4[ret]+lc[ret],AnchoHighest) ?1:0
bottom=-Z4[ret]+lc[ret]<=lowest(-Z4[ret]+lc[ret],AnchoHighest) and -Z4+lc>lowest(-Z4[ret]+lc[ret],AnchoHighest) ?1:0


```
