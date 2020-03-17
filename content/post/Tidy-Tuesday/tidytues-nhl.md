+++
title = "NHL Data & Tidy Tuesday"
date = "2020-03-09"
authors = ["Robin Sifre"]
summary="Exploring the relationship between penalty minutes and goals scores in the NHL."
tags=["tidy tuesday", "R", "statistics", "data science"]

# Featured image thumbnail (optional)
image_preview = ""



+++

I've recently started to participate in [Tidy Tuesday](https://thomasmock.netlify.com/post/tidytuesday-a-weekly-social-data-project-in-r/), a weekly social data project in R. Each week they release a new dataset on their [GitHub](https://github.com/rfordatascience/tidytuesday). It's a fun opportunity to explore new and interesting data sets. After you do a quick analysis and generate some figures, you're supposed to tweet it with #tidytuesday.

{{< tweet 1236043745721712650 >}}


In this post, I walk through a bit of my code, but you can find the complete code on my [GitHub](https://github.com/rrobinn/tidy-tuesday/tree/master/20200303-HockeyGoals).

This week's dataset comes from [HockeyReference.com](https://www.hockey-reference.com/). I used 2 of the downloadable datasets:  
1. Overall career goals.  
2. Season level goals.  

I thought that this multi-level data would be a fun way to explore the impact of how <b> centering variables</b> can clarify which level of analysis is driving the relationship.  


# The question
<b>Is there a relationship between aggressive play (time spent in the penalty box) and scoring?</b>  On the one hand, more aggressive play could mean more goals. On the other hand, too much time in the penalty box takes you out of the game and could minimize your opportunity to score.  

<b> Disclaimer: </b> I know nothing about Hockey, and most of my knowledge comes from the Mighty Ducks franchise. As someone who has lived in Minnesota for four years this is inexcusable, but here we are.  

<table class="image">
<tr><td><img src="/post-img/mighty-ducks.png" alt=" "/></td></tr>
</table>  

<i>Mea culpa.</i>

# Why should I center my variables?
Let's imagine that there is a relationship between penalty minutes and goals scored. You can imagine this relationship work on two different levels: 
You can imagine that the relationship between penalty minutes and goals scored could work on 2 different levels:  
<b> 1. Between-player effect</b>.  More aggressive players score more goals. A relationship between CAREER-AVERAGE penalty minutes and goals would suggest that the relationship is driven by  *between-player* differences.  
<b> 2. Within-player effect</b>. When a given player plays more aggressively, they also score more goals. A relationship between SEASON-AVERAGE penalty minutes and goals would suggest that this relationship is driven by *within-player* differences.  
  
<i>However</i>: when we examine season-averages we are "smushing together" variability driven by season-to-season changes within a player, and variability driven by differences between player skill. In other words, a top player may still score more goals even when they're having a poor season relative to a less skilled player. 

<b>Do aggressive players score more? Or do players score more when they play more aggressively?</b> To better answer this question, we can center our variables.  
If we take each player's season average (for penalty minutes & goals), and subtract it from their career average, we can isolate season-to-season variability. 

# Centering variables
So how did I center my variables? First, I created a variable that holds career-average penalty minutes and goals for each players.  Let's call it `player_stats`.


```r
player_stats = season_goals %>%
  dplyr::select(player, penalty_min, goals) %>%
  group_by(player) %>%
  summarize(ave_penalty = mean(penalty_min), #Career-average stats for player 
            ave_goals = mean(goals))
```

Then, I merged player_stats with `season_goals`, my data.frame that holds season-average goals and penalty minutes. 
```r
merged = merge(season_goals, player_stats, by = 'player')
```



Now creating the <b> centered variables </b> is a piece of cake.  
We center each player's **season-average penalty minutes** (`season_penalty`) on their **career-average penalty minutes** (`ave_penalty`) to create the variable `penalty_c`.  (We do the same thing for goals). 

```r
merged = merged %>%
  mutate(penalty_c = season_penalty - ave_penalty,
         goals_c = season_goals - ave_goals)
```

`penalty_c` now shows how a player's penalty minutes changes from season-to-season, **holding** `ave_penalty` **constant.**  

Negative values of `penalty_c` indicate seasons where a player had <b>lower</b> than average minutes in the penalty box, and positive values indicate  seasons where a player had <b>higher</b> than average minutes in the penalty box. In this case, average refers to their own personal average. 


# What does it buy us?
When we plot <b>season-average</b> penalty minutes against goals scores, it looks like there might be a relationship between these two variables:   

 <table class="image">
<tr><td><img src="/post-img/nhl-uncentered.png" alt=" "/></td></tr>
</table>  

But, it's a bit messy.  In this figure we are smushing together variability between-players (e.g., high-scorers) and variability within a player (e.g., when someone is having a particularly good or bad season).  

Now, let's plot the relationship between these two variables when we center them on a player's career average:  

 <table class="image">
<tr><td><img src="/post-img/nhl-centered.png" alt=" "/></td></tr>
</table>  


Here, the relationship becomes more clear. In a given season, when a player has more penalty minutes than their career average, they also score more goals than their career average.  
Could this just be driven by how much play-time a player gets in a given season? Possibly! But this also illustrates how in this figure we are isolating change within a player, by holding their career averages constant. 