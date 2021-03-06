---
title: "Analyze your Savings Plan recommendations"
date: 2020-04-24T11:16:09-04:00
chapter: false
pre: "<b>3. </b>"
weight: 3
---

We have an understanding of the potential savings available to us, and how we can adjust that based on our business requirements. We also know our usage trends across the business, which will help us with our initial commitment.  We will now go deeper to help you understand exactly what Savings Plan commitment is right for you.

You can think of a single Savings Plan as a highly flexible group of Reserved Instances (RI's), without the same management overhead. Depending on the discount level and your usage, Savings Plans can pay themselves off very quickly and offer large savings, or pay themselves off over a longer period with less savings. We will look into a Savings Plan to ensure our commitment pays off in the right amount of time and offers the amount of savings we need.  

We will analyze our Savings Plan to further refine our initial commitment level to purchase, this commitment will be very low risk and high return. Once that is purchased you then re-analyze every couple of weeks or every month and "top up" your commitment levels. This ensures you maintain high levels of discounts, and you can continually adjust as your business evolves.

1. Click on **Recommendations** and select **EC2 Instance Savings Plans**, **1-year**, **No upfront**, **30 days**:
![Images/AnalyzeSP1.png](/Cost/100_3_Pricing_Models/Images/AnalyzeSP1.png?classes=lab_picture_small)
If **Payer** is selected and you see few or no recommendations, select **Linked account** to display recommendations to the linked accounts within your AWS Organization.

2. Scroll down and click **Download CSV**
![Images/AnalyzeSP2.png](/Cost/100_3_Pricing_Models/Images/AnalyzeSP2.png?classes=lab_picture_small)

3. There is a sample file here if you do not have data:

    - [Sample Savings Plan](/Cost/100_3_Pricing_Models/Code/SavingsPlan.xlsx)

4. Add the new column headings **O**, **P** and **Q**. and put in the formulas for each:
    - Monthly OnDemand Cost, **Cell O2**: **=G2*730**
    - Monthly Cost after SP, **Cell P2**: **=O2-K2**
    - Fully Paid Day, **Cell Q2**: **=P2*12/O2**
    - [Updated Sample Savings Plan](/Cost/100_3_Pricing_Models/Code/SavingsPlan02.xlsx)
    ![Images/AnalyzeSP3.png](/Cost/100_3_Pricing_Models/Images/AnalyzeSP3.png)

5. The **Fully Paid Day** is the number of months it takes to pay off the entire 12 month savings plan. It is a combination of the discount level and your utilization level. At your current usage, after this day even if you turn off all your usage you will not lose money and be better off than paying on demand. The sooner the period the lower risk the purchase.
![Images/AnalyzeSP4.png](/Cost/100_3_Pricing_Models/Images/AnalyzeSP4.png)

6. We want the lowest risk purchases for our initial commitment, so sort by the **Fully Paid Day**, in order of **smallest to largest**, and insert some blank lines before a fully paid day of **9 months**:
    - [Updated Sample Savings Plan](/Cost/100_3_Pricing_Models/Code/SavingsPlan03.xlsx)
    ![Images/AnalyzeSP5.png](/Cost/100_3_Pricing_Models/Images/AnalyzeSP5.png)

7. Sort the top group and bottom group by **Estimated monthly savings amount**, in order of **largest to smallest**, insert some lines above anything less than $50 in savings:
    - [Updated Sample Savings Plan](/Cost/100_3_Pricing_Models/Code/SavingsPlan04.xlsx)
    ![Images/AnalyzeSP6.png](/Cost/100_3_Pricing_Models/Images/AnalyzeSP6.png)

8. You now have four groups of Savings Plan usage:
    - Very low risk, high return
    - Very low risk, low return
    - low to medium risk, high return
    - low to medium risk, low return

9. Combining this information with the previous exercises, your initial purchase will be typically focused on the low risk and high return, and some of the medium risk high return. Add up the hourly commitment for the recommendations that match your business requirements. In this example we have taken all of the very low risk high return, and 40% of the medium risk high return:  
    - [Updated Sample AnalyzeSP](/Cost/100_3_Pricing_Models/Code/SavingsPlan05.xlsx)
    ![Images/AnalyzeSP7.png](/Cost/100_3_Pricing_Models/Images/AnalyzeSP7.png)

10. Take this commitment level, apply the findings from the previous exercises (type of Savings Plan and Usage Trend) to make your initial purchase.

{{< prev_next_button link_prev_url="../2_usage_trend/" link_next_url="../4_visualize_recommendations/" />}}
