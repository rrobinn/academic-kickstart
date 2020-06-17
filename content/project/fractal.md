+++
title = "Finding structure in the noise: What the fractal structure of eye-tracking time series can tell us about attention"
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
#image = "sample_et.png"
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

