+++
title = "Finding structure in the noise: Complexity & visual attention"
date = "2020-06-17"

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = [" Robin Sifre", "Isabella Stallworthy", "Daniel Berry", "Jed Elison"]


# Featured image thumbnail (optional)
image_preview = ""


# Does the content use math formatting?
math = true

# Does the content use source code highlighting?
highlight = true

# Featured image
# Place your image in the `static/img/` folder and reference its filename below, e.g. `image = "example.jpg"`.
[header]
image = "eye-tracking-emory.jpg"
caption = ""


+++

# Background  
An infant sits in daycare when she hears her mother’s voice. She immediately stops playing with her blocks, and a flurry of coordinated attention processes begin to coordinate in her brain. She must disengage from the enticing blocks, and search for her mother amidst a room filled with competing distractors. This seemingly simple behavior requires the recruitment – and the coordination of – multiple developing attention processes.

<i>Coordination</i> is the organization of different parts of a complex system that enable them to effectively work together. Coordination is essential to cognition but has been relatively understudied (Van Orden, et al., 2011). Research on attention is no exception. While we have a clear picture of the developmental timeline of each sub-component of attention, little is known about how these processes become coordinated.

{{< figure library="true" src="sample_et.png" title="Eye-tracking data. Pink blobs show where infant is looking" lightbox="true" >}}

# My work
I fill this gap by applying methods from Complexity Science to study infant attention. Complexity Science is concerned with quantifying the dynamics of complex systems composed of multiple interacting parts.  

I measure the overall complexity and coordination of infants’ attention by quantifying the <i>fractality</i> of their eye-gaze. Fractality refers to nested patterns of variability that are apparent across multiple measurement scales, resulting in a <i>self-similarity</i> over time (Van Orden et al., 2011). <u>Fractal organization is a critical feature of healthy cognitive and psychobiological systems. It is thought to reflect coordinated systems that are highly self-organized, yet also flexible to change</u>.  

This approach leverages eye-tracking time series data to infer the extent to which interactions between these sub-processes are well-coordinated. Research with adults has shown that they are faster to find target objects when their eye-gaze shows these fractal signatures, suggesting that flexible coordination between attention sub-processes is critical for efficient visual exploration (Aks et al., 2002).  


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

