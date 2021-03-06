---
title: "Finding structure in the noise: Complexity & visual attention"
summary: Applying methods from Complexity Science to Understand Infant Attention
tags:
- eye-tracking
date: "2020-09-14"

# Optional external URL for project (replaces project detail page).
external_link: ""

image:
  caption: ""
  focal_point: Smart

links:
#- icon: twitter
#  icon_pack: fab
#  name: Follow
#  url: https://twitter.com/georgecushen
url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: example
---

# Background  
An infant sits in daycare when she hears her mother’s voice. She immediately stops playing with her blocks, and a flurry of coordinated attention processes begin to coordinate in her brain. She must disengage from the enticing blocks, and search for her mother amidst a room filled with competing distractors. This seemingly simple behavior requires the recruitment – and the coordination of – multiple developing attention processes.

<i>Coordination</i> is the organization of different parts of a complex system that enable them to effectively work together. Coordination is essential to cognition but has been relatively understudied (Van Orden, et al., 2011). Research on attention is no exception. While we have a clear picture of the developmental timeline of each sub-component of attention, little is known about how these processes become coordinated.

{{< figure library="true" src="sample_et.png" title="Eye-tracking data. Pink blobs show where infant is looking" lightbox="true" >}}

# My work
I fill this gap by applying methods from <b>Complexity Science</b> to study infant attention. Complexity Science is concerned with quantifying the dynamics of complex systems composed of multiple interacting parts.  

I measure the overall complexity and coordination of infants’ attention by quantifying the <i>fractality</i> of their eye-gaze. Fractality refers to nested patterns of variability that are apparent across multiple measurement scales, resulting in a <i>self-similarity</i> over time (Van Orden et al., 2011). <u>Fractal organization is a critical feature of healthy cognitive and psychobiological systems. It is thought to reflect coordinated systems that are highly self-organized, yet also flexible to change</u>.  

This approach leverages eye-tracking time series data to measure <b>eye-gaze fractality</b> as a proxy for attention coordination. Research with adults has shown that they are faster to find target objects when their eye-gaze shows these fractal signatures, suggesting that flexible coordination between attention sub-processes is critical for efficient visual exploration (Aks et al., 2002).  

## The experiment  
{{< figure library="true" src="experiment.png" title="Experimental set-up" lightbox="true" >}}  

We had infants come to the lab, and watch a series of movies:  
1. <b>Social movies</b>: Videos of ladies dancing with toys. Babies love these movies.  
2. <b>Pixelated movies</b>: These were the same as the social movies, except that the dancing ladies were pixelated. The idea here is that we wanted to preserve a lot of the low-level visual information, but remove most of the socially-engaging information.  
3. <b>Attention Cues</b>: Throughout the experiment, we show babies attention cues to make sure that they are still calibrated to the eye-tracker. We decided to also measure their eye-gaze fractality during these trials as a "baseline" (e.g. how well coordinated is attention when there a simplistic shape on the screen?).  
  
We predicted that:  
1. As babies got older, their eye-gaze would become increasingly fractal, indexing their increasingly coordinated attention abilities.  
2. Babies' eye-gaze would be more fractal during the social movies, when they would be more engaged/attentive.  
3. Babies' eye-gaze should also change on a moment-by-moment basis - they should be more fractal when they were paying attention to important information.  

## What did we find?

# Find out more  
For more information on this project, please check out [my github](https://github.com/rrobinn/fractal-eye-analyses).  

Here you'll find nitty-gritty information on how I:  
1. Created time series from 300 Hz eye-tracking data.  
2. Used  [Multifractal Detrended Fluctuation Analysis](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3366552/) to calculate the fractality of each time series.  
3. Built statistical model of how babies' attention becomes more coordinated during the first years of life.  

(Here's a sneak peak).  

{{< figure library="true" src="xy_coord.png" title="Step 1. Extract (x,y) coordinates of where infant is looking" lightbox="true" >}}
{{< figure library="true" src="amplitude.png" title="Step 2. Create unidimensional time series by calculating amplitude (e.g. change in eye-gaze position from one moment to the next)" lightbox="true" >}}
{{< figure library="true" src="palmer_fig1.png" title="Step 3. Figure from Palmer et al. (2018). (a) Simulated time series noises. (b) 'Power law' relation between power and frequency of fluctuations in respective time series. Scaling exponents close to 1 (Pink Noise) indicate a fractal structure." lightbox="true" >}}

