+++
title = "Tidy Tuesday"
date = "2020-03-09"

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = ["Robin Sifre"]

summary=""



# Featured image thumbnail (optional)
image_preview = ""


+++

I've recently started to participate in [Tidy Tuesday](https://thomasmock.netlify.com/post/tidytuesday-a-weekly-social-data-project-in-r/), a weekly social data project in R. Each week they release a new dataset on their [GitHub](https://github.com/rfordatascience/tidytuesday). It's a fun opportunity to explore new and interesting data sets.  In this post, I walk through a bit of my code, but you can find the complete code on my [GitHub](https://github.com/rrobinn/tidy-tuesday/tree/master/20200303-HockeyGoals).

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
**Mea culpa.**

Anyway, I thought it would be neat to investigate the relationship between <b>Penalty minutes</b> and <b> goals scored by player</b>. 

# Do aggressive players score more? Or do players score more when they play more aggressively?
You can imagine that the relationship between penalty minutes and goals scored could work on 2 different levels:  
<b> 1. Between-player effect</b>.  Hypothesis: More aggressive players score more goals. A relationship between *career average* penalty minutes and *career average* goals would suggest that the relationship is driven by  *between-player* differences.  
<b> 2. Within-player effect</b>. Hypothesis: When a given player plays more aggressively, they also score more goals. A relationship between penalty minutes and goals *adjusted for the player's career averages* would suggest that this relationship is driven by *within-player* differences.

# Centering variables
So how did I center my variables? First, I created <mark>player_stats</mark>, a variable that holds career-average penalty minutes and goals for each players.  

{{< highlight go "linenos=table, linenostart=1" >}}
player_stats = season_goals %>%
  dplyr::select(player, penalty_min, goals) %>%
  group_by(player) %>%
  summarize(ave_penalty = mean(penalty_min),
            ave_goals = mean(goals))
{{< / highlight >}}

Then, I merged player_stats with <mark>season_goals</mark>.
{{< highlight go "linenos=table, linenostart=1" >}}
merged = merge(season_goals2, player_stats, by = 'player')
{{< / highlight >}}  

Now we are ready to create our <b> centered variabes </b>. We center each player's **season-average penalty minutes** (<mark>season_penalty</mark>) on their **career-average penalty minutes** (<mark>ave_penalty</mark>) to create the variable <mark>penalty_c</mark>.  
<penalty_c> now shows how a player's penalty minutes changes from season-to-season, **holding <mark>ave_penalty</mark> constant.  
Negative values of <mark>penalty_c</mark> indicate seasons where a player had <b>lower</b> than average minutes in the penalty box, and positive values indicate  seasons where a player had <b>higher</b> than average minutes in the penalty box. In this case, average refers to their own personal average. 

{{< highlight go "linenos=table, linenostart=1" >}}
merged = merged %>%
  mutate(penalty_c = season_penalty - ave_penalty,
         goals_c = season_goals - ave_goals,
{{< / highlight >}}  


  
  