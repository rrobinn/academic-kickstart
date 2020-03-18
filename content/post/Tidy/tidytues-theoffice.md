+++
title = "Tidy Text Mining with The Office"
date = "2020-03-12"
authors = ["Robin Sifre"]
summary="My first venture into text mining"
tags=["tidy tuesday", "R", "ggplot", "data science"]
categories=["Tidy Tuesday"]
# Featured image thumbnail (optional)
image_preview = ""

+++

With all of the COVID-19 related stress and my quickly-emerging cabin fever, I was glad to see that this week's [Tidy Tuesday](https://thomasmock.netlify.com/post/tidytuesday-a-weekly-social-data-project-in-r/) was a light-hearted dataset. This week we using the [schrute package](https://bradlindblad.github.io/schrute/index.html). As stated in the documentation:  

<i>"The schrute package has one and only one purpose: share the complete script transcription for The Office (US) television show. Users are encouraged to use the tidy text data for exploration, learning and fun."</i>  

Rather than try to investigate hard-hitting questions about whether Michael's incompetency predicts output at Dunder Mifflin, I decided to use this opportunity to familiarize myself with `tidytext`, a package designed for text mining. This [vignette](https://cran.r-project.org/web/packages/tidytext/vignettes/tidytext.html) is a great introduction.  

# The data
Let's take a look at the data.  

```r
glimpse(schrute)
Observations: 55,130
Variables: 12
$ index            <int> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, …
$ season           <chr> "01", "01", "01", "01", "01", "01", "01", "01", "01", "01", "01", "01", "01…
$ episode          <chr> "01", "01", "01", "01", "01", "01", "01", "01", "01", "01", "01", "01", "01…
$ episode_name     <chr> "Pilot", "Pilot", "Pilot", "Pilot", "Pilot", "Pilot", "Pilot", "Pilot", "Pi…
$ director         <chr> "Ken Kwapis", "Ken Kwapis", "Ken Kwapis", "Ken Kwapis", "Ken Kwapis", "Ken …
$ writer           <chr> "Ricky Gervais;Stephen Merchant;Greg Daniels", "Ricky Gervais;Stephen Merch…
$ character        <chr> "Michael", "Jim", "Michael", "Jim", "Michael", "Michael", "Michael", "Pam",…
$ text             <chr> "All right Jim. Your quarterlies look very good. How are things at the libr…
$ text_w_direction <chr> "All right Jim. Your quarterlies look very good. How are things at the libr…
$ imdb_rating      <dbl> 7.6, 7.6, 7.6, 7.6, 7.6, 7.6, 7.6, 7.6, 7.6, 7.6, 7.6, 7.6, 7.6, 7.6, 7.6, …
$ total_votes      <int> 3706, 3706, 3706, 3706, 3706, 3706, 3706, 3706, 3706, 3706, 3706, 3706, 370…
$ air_date         <fct> 2005-03-24, 2005-03-24, 2005-03-24, 2005-03-24, 2005-03-24, 2005-03-24, 200…
```
What we have is every line (`text`) spoken by every `character` organized by `episode` and `season`. 

# Prepping the data
First, I used `unnest_tokens` to split the `text` variables so that each word token had it's own row.  After that, I removed the stop_words (e.g. words that are not useful for analyses, like "the" and "a")
```r
# Tokenize dialogue 
token.schrute = schrute %>%
  tidytext::unnest_tokens(word, text)
dplyr::glimpse(token.schrute) #570,450 observations

stop_words = tidytext::stop_words
tidy.token.schrute = token.schrute %>%
  dplyr::anti_join(stop_words, by = 'word') 
```
