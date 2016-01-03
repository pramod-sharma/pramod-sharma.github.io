---
layout: post
comments: true
title:  "AWS provisioned IOPS vs RAID 5 based setup"
date:   2015-12-25 01:15:00
categories: AWS, Startup
---

As all of us know General purpose SSD based EBS comes with 3 IOPS per GB which may shoot upto 3000 IOPS on the basis of your Physical Rack, which is too less for the cases of Big Data and IOT Solutions where IOPS may
shoot well over it.

AWS has launched the provision of Provisioned IOPS for such cases. But in such cases you have to shell out extra for IOPS which was $0.065 per provisioned IOPS-month at the time of writing article, which is an extra overhead for your buzzing startup. So in such cases one may go for RAID 5

Lets firstly see how RAID handles it(talk specifically about RAID 5) - RAID 5 uses striping for increasing data redundancy thus increasing overall performance for fetching data segments and Parity increase data resiliency. 

<b>Now lets discuss both options and their costs for my 250 GB setup:-</b>

* Option 1 :- Implement (250 GB provisioned IOPS setup) for a month with 15000 IOPS.
              My Cost will be 0.125 * 250 (Fixed cost of storage) + 0.065 * 15000 (Provisioned IOPS SSD cost) bringing total to $995

* Otion 2 :- Implement RAID 5 with 4 General Purpose SSDs each of 95GB with Read percentage of 70% and write percentage of 30%.
             My Cost will be 95 * 4 * 0.10 = $38.
             It can substain 21000 IOPS on SSD
             You can go for even more IOPS incase you go for RAID10, so its all upto you(but it will cost you more space)

For Linux one may use <b>mdadm</b> to setup RAID servers. <a href='http://www.tecmint.com/author/babinlonston/'> Babin Lonston </a> has wrote one cool article for it <a href='http://www.tecmint.com/create-raid-5-in-linux/'>here</a>. You may go for it
To calculate your RAID Setup requirement use calculator <a href='http://www.thecloudcalculator.com/calculators/disk-raid-and-iops.html'> here </a>

But remeber it all depends on your needs. Please comment incase you find any issue with this approach.

