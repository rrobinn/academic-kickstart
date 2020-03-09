+++
title = "Tidy Tuesday"
date = "2020-03-09"

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = ["Robin Sifre"]

summary=""



# Featured image thumbnail (optional)
image_preview = ""


+++

I've recently started to participate in [Tidy Tuesday](https://thomasmock.netlify.com/post/tidytuesday-a-weekly-social-data-project-in-r/), a weekly social data project in R. Each week they release a new dataset on their [GitHub](https://github.com/rfordatascience/tidytuesday). It's a fun opportunity to explore new and interesting data sets.  

This week's dataset comes from [HockeyReference.com](https://www.hockey-reference.com/). There were 3 downloadable datasets:  
1. Overall career goals.  
2. Season level goals.  
3. Game level goals.  

I thought that this multi-level data would be a fun way to explore the impact of how <b> centering variables</b> can clarify the relationship between two variables - specifically, which level of analysis is driving the relationship?     

# The question
<b> Disclaimer: </b> I know nothing about Hockey, and most of my knowledge comes from the Mighty Ducks franchise. I hear that as someone who has lived in Minnesota for four years this is inexcusable, but here we are.  

<table class="image">
<tr><td><img src="/post-img/mighty-ducks.png" alt=" "/></td></tr>
</table>  
*Mea culpa.*    

Anyway, I thought it would be neat to investigate the relationship between <b>Penalty minutes</b> and <b> goals scored by player</b>. 

# Do aggressive players score more? Or do players score more when they play more aggressively?
You can imagine that the relationship between penalty minutes and goals scored could work on 2 different levels:  
<b> 1. Between-player effect</b>.  Hypothesis: More aggressive players score more goals. A relationship between *career average* penalty minutes and *career average* goals would suggest that the relationship is driven by  *between-player* differences.  
<b> 2. Within-player effect</b>. Hypothesis: When a given player plays more aggressively, they also score more goals. A relationship between penalty minutes and goals *adjusted for the player's career averages* would suggest that this relationship is driven by *within-player* differences.

# Centering variables
{{< highlight go "linenos=table,hl_lines=8 15-17,linenostart=199" >}}
a = data$test
{{< / highlight >}}

  
  