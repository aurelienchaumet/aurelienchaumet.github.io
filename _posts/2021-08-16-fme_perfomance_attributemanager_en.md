---
layout: single
permalink: /articles/fme_performance_attributemanager_en/
title : "FME : Comparative performance test between AttributeManager and some equivalent transformers" 
header:
  overlay_image: https://dl01fbzxdpfby.cloudfront.net/images/fme/performance_attributemanager/fme_lizard_perf.png
  overlay_filter: 0.3
  teaser: https://dl01fbzxdpfby.cloudfront.net/images/fme/performance_attributemanager/fme_lizard_perf.png
excerpt:
  Can only performance explain the cohabitation of several equivalent FME transformers ?

og_image: https://dl01fbzxdpfby.cloudfront.net/images/fme/performance_attributemanager/fme_lizard_perf.png

comments: true
share: true
toc: true
toc_label: "Plan"
toc_icon: "chart-line"
toc_sticky: true
---

Vous trouverez une [version française de cet article ici](/articles/fme_performance_attributemanager_fr/) :smirk:

The [AttributeManager](https://docs.safe.com/fme/html/FME_Desktop_Documentation/FME_Transformers/Transformers/attributemanager.htm) is a transformer present in the toolbox of any good FMEist **since 2016**.

It allows :

- **rename** attributes
- **delete** attributes
- **create** attributes
- **defines values of an attribute** whether by arithmetic operation, conditional values or concatenation of fields

Before 2016, each of these functions was possible in FME through **special transformers** ; AttributeCreator allows, for instance, create new attributes and AreaCalculator calculate polygons area.

We might therefore think, that 5 years after its release, users have become accustomed to its operation (which is true largely in view of [its 2nd place in transformers ranking](https://aurelienchaumet.github.io/articles/fme_transformers_classement/#attributemanager-passe-second)), and Safe should decide to **abandon his predecessors**.

But this is not the case, they continue to live happily together.

## Why a speed test ?

So I’m making the assumption that based on the use cases, **_performance must not be the same_**. This could explain why transformers, having similar functions, still exist in parallel.

Let’s take a closer look at this, taking, for the test, 4 transformers that the AttributeManager could replace functionally speaking :

- [AttributeRenamer](https://docs.safe.com/fme/html/FME_Desktop_Documentation/FME_Transformers/Transformers/attributerenamer.htm), to rename attributes
- [AttributeCreator](https://docs.safe.com/fme/html/FME_Desktop_Documentation/FME_Transformers/Transformers/attributecreator.htm), to create new attributes
- [AttributeKeeper](https://docs.safe.com/fme/html/FME_Desktop_Documentation/FME_Transformers/Transformers/attributekeeper.htm), which just keep some attributes
- [AreaCalculator](https://docs.safe.com/fme/html/FME_Desktop_Documentation/FME_Transformers/Transformers/areacalculator.htm), allows to calculate polygons area

To carry out this test, I get [Charente-Maritime PCI parcels (Plan Cadastral Informatisé)](https://cadastre.data.gouv.fr/data/etalab-cadastre/2021-04-01/geojson/departements/17/), nearly 1Go of data, with 1 671 935 lines.
{: .notice--info}

_We will call the AttributeManager transformer *AM* in the rest of this article to avoid overloading the reading._

You will find the workbench that allowed me to perform the performance tests [here](aurelienchaumet.github.io/data/fme/).

## Test of the AM face to face with its ancestors

To try to save some time, [Feature Caching](https://www.safe.com/blog/2018/05/caching-data-fme-evangelist174/) is enabled for all of the following tests only after reading the input data.  
Each time a process test is indicated, I ran the same transformer (or chain of transformers) 5 times and averaged the 5 times.

Regarding the AM facing its anchors, one by one, and for the same tasks, you will find the summary of times below :

![1V1 comparison](https://dl01fbzxdpfby.cloudfront.net/images/fme/performance_attributemanager/1V1_en.png "1V1 Comparison"){: .align-center}

For the moment, except for the creation of attributes where a doubt may remain (the gap is rather small), **the "old" specific transformers appear as more efficient than the AM**.

It’s like having a [Leatherman](https://en.wikipedia.org/wiki/Leatherman) and a Phillips screwdriver on hand, and you only have Phillips screws to put on. You’ll probably go faster using the screwdriver.

## AM test to replace a chain of predecessors

Let’s now perform sequences of the previous 4 transformers compared to the same tasks performed in the AM.

First of all, it should be noted that a single AM may, at times, not perform the same functions as single-spot transformers.  
For example, if you want to create a new Attribute 2 from an already existing Attribute 1, and delete Attribute 1 in the stride.
Just chain an AttributeCreator and then an AttributeRemover (or AttributeKeeper for those who like to check a lot of boxes:smile:).  
Here, one AM is not enough.  
Indeed, if you say in the AM parameters that you want to both create a field from an attribute and delete it, it may not understand what you want it to do...
{: .notice--info}

2 transformers chain :

![2V1 comparison](https://dl01fbzxdpfby.cloudfront.net/images/fme/performance_attributemanager/2V1_en.png "2V1 comparison"){: .align-center}

3 transformers chain :

![3V1 comparison](https://dl01fbzxdpfby.cloudfront.net/images/fme/performance_attributemanager/3V1_en.png "3V1 comparison"){: .align-center}

4 transformers chain :

![4V1 comparison](https://dl01fbzxdpfby.cloudfront.net/images/fme/performance_attributemanager/4V1_en.png "4V1 comparison"){: .align-center}

We realize here, that **when at least 2 historical transformers are chained, against a single AM, the time saving is there**.  
And it can sometimes even be 2x times faster!

I guess that the AM is optimized, when there are several tasks to perform, so that they are carried out as quickly as possible.

To use the Leatherman metaphor, if you have to screw in cruciforms, straighten a rod and open a beer (it can!), this time you’ll save time by taking the Leatherman, rather than picking up each tool one by one from your toolbox.

## AM Chain test

A last test to push a little...

What happens if we find ourselves in the case of figure mentioned above of the creation of an Attribute 1 and an Attribute 2, then of an Attribute 3, itself dependent on the first 2, but that we wish to exchange with the deletion of the first 2 created attributes?

Clearly, an AttributeCreator + an AttributeKeeper do the trick.  
But if we want to go through AM, we will have to chain 2:

- AttributeCreator (creation of Attribute 1, Attribute 2 and Attribute 3 = Attribute 1 + Attribute 2) + AttributeKeeper (we just keep Attribute 3) : 139 seconds
- AM which create the 3 attributes + AM which keeps only Attribute 3 : 148 seconds

Logically enough, **the chain of 2 AM is longer than that of 2 historical transformers**.

If you want to use 2 different Leathermans, each for different tasks, you might as well take the specific tools, and you will save time!

## Conclusion

After these few quick tests, I think there is some truth in my initial hypothesis.

In fact, it is in our best interest to use a **transform history** AttributeWhat rather than the AM, only if **a single operation** is performed.

Therefore, as **several operations** are chained, we must not deprive ourselves of using the**AttributeManager** directly in order to save processing time!!

**_Leatherman Metaphore_**. I rest my case...

![gif barack obama drop the mic](https://media.giphy.com/media/3o7qDEq2bMbcbPRQ2c/giphy.gif "Barack drops the mic"){: .align-center}

Even if it is always good tone to be wary of the order in which the operations are carried out.  
As mentioned earlier, avoid, for example, in the same AM deleting an attribute if you want to perform a field calculation or concatenation on it :smirk:.

----

Feel free to comment directly below, or send me a [message on Twitter](https://twitter.com/messages/compose?recipient_id=938055192221765634), I will answer you with pleasure :pray: !
