---
title: Long Needed Aquarium Water Chemistry Adjustments
date: 2025-12-13
draft: false
tags:
  - blog
  - aquarium
---

# Background

I have a 135gal saltwater aquarium in my office full of coral and several fish. The system is fairly automated, it is controlled by a commercially available aquarium controller running custom rules that I have programmed into it to control heaters, supplement dosing, pumps, UV sterilizer, Ozone reactor, etc. I'll probably make a post at some point in the future explaining the setup.

The supplement dosing is the trickiest part of the whole system, it requires constant water parameter testing to ensure that the correct amount of supplements  are being dosed, and I also have to ensure that I don't run out of the supplements. As I get busy with life, kids, work, etc, inevitably I forget to check the containers of supplements and the system doses nothing to the tank for days or weeks until I remember to check them.

This post is about the multiday process of fixing this problem.

## Steps

1. Check the Alkalinity, Calcium, and Magnesium levels
2. Determine to bolus amount required to adjust the levels to the correct values
3. Dose the bolus amount (possibly over a few days depending on the amount)
4. Check the levels again
5. Wait 24 hours and check the levels again
6. Calculate the amount needed for a daily dose based on the test results
7. Setup dosing for the new amount
8. Check the values every day for several days to make sure the values are staying stable
9. Repeat steps 6-8 until a stable daily value is achieved


!![Image Description](/images/Pasted%20image%2020251213102645.png)


!![Image Description](/images/Pasted%20image%2020251213102700.png)


# Calculation


`Amount Needed = ( (Target value - Current value) * Total Water Volume ) / (Concentration of Additive)`


# Results

I have an automated water tester set up on the system, it checks Alkalinity once every 6 hours and Calcium and Magnesium once ever 12 hours (Ca and Mg levels are dependent on the Alk level, so changes in Alk are more important to monitor as it would be an indicator that Ca/Mg levels will be changing. Checking Ca/Mg less often saves on testing reagent).

As you can see from the graph of the Alkalinity level, the value was sitting at about 5.00 dKH (Degrees of German carbonate hardness). After the bolus dose, I was able to bring the value up to about 10.5 dKH. The ideal range for Alkalinity is between 8 and 12 dKH,  I decided that I'd settle for around 9.5 dKH so as to conserve the Alk supplement. There is a little bit of wiggle room in the calculation and dosing implementation due to the actual water volume being unknown (this is because 135gal is an estimate based on the size of the aquarium and the size of the sump in the stand that holds most of the filtration, the water volume in the sump is hard to calculate because it has multiple chambers of varying water levels). The wiggle room results in some slop in the calculation as can be seen below. 
### Alk Supplement Calculation

*Note: 135gal = 511L*

`Bolus Amount = ((10.0dKH - 5.0dKH) * 511L) / 33.3g/L (*Dry Sodium Bicarbinate*) = 76.7 grams`

`Daily Dose Amount = ((9.5dKH - 8.4dkH)) / 0.005g/mL (*Liquid Sodium Bicarbinate*)  = 212m/L per day`

!![Image Description](/images/Pasted%20image%2020251213105633.png)

The same approach was taken with the Ca level, but I am still in the process of monitoring the Ca level over the course of a few days to ensure the dosage is correct. I do not automatically dose Mg as the values normally remain fairly stable, if adjustments are needed, I manually dose an amount using the same calculation.


!![Image Description](/images/Pasted%20image%2020251213105701.png)