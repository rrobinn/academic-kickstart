+++
title = "College Tuition & Career Earnings"
date = "2020-03-12"
authors = ["Robin Sifre"]
summary=""


# Featured image thumbnail (optional)
image_preview = ""

+++

I've recently started to participate in [Tidy Tuesday](https://thomasmock.netlify.com/post/tidytuesday-a-weekly-social-data-project-in-r/), a weekly social data project in R.  

This week, they shared an extremely rich dataset (you can find it [here](https://github.com/rfordatascience/tidytuesday/tree/master/data/2020/2020-03-10), on college tuition, diversity, and salary. There was so much more I wanted to do with this data, but because I still have my PhD to finish, I limited myself. At the bottom of [my code](https://github.com/rrobinn/tidy-tuesday/tree/master/20200310-Tuition-Diversity) I commented out some interesting relationships between <b>tuition</b> and <b>diversity</b> that I didn't have time to pursue.  

Here are some tweets from people who did pursue these questions:

{{< tweet 1238053882762321921 >}}
{{< tweet 1237769330336595969 >}}


# The question(s) 
- We know that tuition has been rising - but is this true when we adjust for inflation? Is this driven by public or private schools?  
- What is the relationship between tuition and salary?

# The rise of tuition
To answer this, I used the `historical_tuition` data, which has average college tuition data from 1985. I decided to look at <b> dollar inflation adjusted</b> tuition to aid in interpretability. 

```r
historical_tuition %>% 
  filter(tuition_type == 'All Constant') %>%# dollar inflation adjusted     
ggplot(data = ., aes(x = yr, y = tuition_cost, group_by(type), color = type) ) + 
  geom_point() +
  geom_line() + 
  theme_bw() + 
  theme(legend.background = NULL) +
  xlab('Year') +
  ylab('Tution ($ inflation adjusted)') + 
  scale_x_continuous(breaks = seq(1985, 2015, 5))
```

<table class="image">
<tr><td><img src="/post-img/tuition-increase.png" alt=" "/></td></tr>
</table>  