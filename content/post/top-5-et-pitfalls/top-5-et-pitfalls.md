+++
title = "Top 5 Eye Tracking Fails"
date = "2020-03-12"
authors = ["Robin Sifre"]
summary="How to avoid them"


# Featured image thumbnail (optional)
image_preview = ""

+++

I've worked with a lot of eye tracking data, and have reviewed a lot of academic papers that use eye-tracking. 

This method is fantastic - I'm not exaggerating when I say that we wouldn't know half the things we do about infant cognition without it. It also is a great tool for studying non-verbal populations.  

BUT, I've learned a few lessons over the years, some of them the hard way. I thought I'd share them here to help others who use, or are thinking of using, eye tracking. 

I present: <b> Top 5 Eye Tracking Fails and How to Avoid Them </b>.

# 1. You haven't assessed the quality of your data.  
This is especially important when you are working with a population with noisier data (I'm lookin at you, babies), but is critical no matter what. Without knowing whether the data are high quality, you don't know if you can trust it.  Being able to trust your data is critical, and everything on this list is really just a variant of that. 

<table class="image">
<caption align="bottom">Imagine looking at these bad boys for 45 minutes.
</caption>
<tr><td><img src="/post-img/trust-issues.png" alt=" "/></td></tr>
</table>  

Here are some things I always, always (always) investigate:  
- [x] What is the % of samples with high-quality data? Most eye-trackers provide an estimate of data quality for each sample. I make sure that most of my samples have accurate recordings.  
- [x] How noisy are my data? A quick and dirty way to do this is to calculate the root-mean-square-error of each fixation. Ideally, you don't want this to be high - if it is, it means the "best guess" of where the infant is looking is not smooth, and looks really "jumpy" which is no bueno.  
- [x] How much data do I even have? It's pretty easy to not realize that you are making inferences from trials with 90% missing data. Make sure you know how much missing data you have.  

# 2. You haven't established how much data is enough.  
This one is pretty common. Missing data is to be expected. With babies, you're going to have a lot of missing data. But it's critical that you decide ahead of time how much missing data is too much missing data.  
We're trying to make inferences about a person's mental state based on where they are looking on a computer screen. Don't make this even more sketchy by making this inference based on 2 seconds of data.  

# 3. Calibration draft!  
Before collecting eye tracking data, you need to "calibrate" a person to the eye-tracker. Lots of studies make sure that the calibration is good at the beginning, press "go" and move on. Sadly, calibration drift is a thing, and I highly recommend that you validate the calibration throughout the experiment. Again, this is a [bigger issue in kids than adults](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5974590/) but an issue for everyone.  

#4. Waning attention.  
Man, some eye tracking tasks are BORING. If you pay an undergrad $10 to stare at a black and white display of faces for 45 minutes, they're going to zone out. Always check that your effects aren't mainly driven by time (e.g. increasing boredom). 

<table class="image">
<caption align="bottom">Imagine looking at these bad boys for 45 minutes.
</caption>
<tr><td><img src="/post-img/faec-et.png" alt=" "/></td></tr>
</table>  

#5. Quality is correlated with your outcome or varies by group.
Let's say you're comparing 5-year-olds to 10-year-olds, and find that 10-year-olds are way better at a visual search task. Time to publish, right? Not so fast! You need to make sure that your results aren't driven by differences in data quality. Otherwise, you <i>think</i> you're seeing a cool developmental trend, but you're really just looking at how eye tracking data quality improves with age.  

It's actually ok if there are differences in data quality! Just include quality covariates in your statistical model so that you're controlling for them. 