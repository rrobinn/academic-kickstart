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
First, I used `unnest_tokens` to split the `text` variable so that each word is in its own row.  This turns streams of dialogue into more manageable "tokens." 
```r
# Tokenize dialogue 
token.schrute = schrute %>%
  tidytext::unnest_tokens(word, text)
dplyr::glimpse(token.schrute) #570,450 observations
```

After that, I used `stop_words` to generate a list of <b>stop words</b>. These are words that are not useful for analyses (like "the" and "a").



```r
stop_words = tidytext::stop_words
tidy.token.schrute = token.schrute %>%
  dplyr::anti_join(stop_words, by = 'word') 
```
{{% alert note %}}
Here I used `anti_join` to return all rows from `token.schrute` that do NOT have matching values in `stop_words`.  
{{% /alert %}}

Now that we've removed the stop words, we can visualize the most common words in this dataset. 



```r
tidy.token.schrute %>%
  dplyr::count(word, sort = TRUE) %>%
  dplyr::filter(n > 400) %>%
  dplyr::mutate(word = stats::reorder(word, n)) %>%
  ggplot2::ggplot(ggplot2::aes(word, n)) +
  ggplot2::geom_col() +
  ggplot2::xlab(NULL) +
  ggplot2::coord_flip() +
  ggplot2::theme_minimal()
```
{{% alert note %}}
You can use `reorder` to order your geom_col() figure. Otherwise, the bars will not be in order based on
{{% /alert %}}


{{< figure library="true" src="Most_used_words.pdf" title="Most used words" lightbox="true" >}}


# Positive vs Negatively charged words
Now things get interesting! `tidytext` has a function called `get_sentiments` that provides a dictionary of words, and whether they have a positive or negative connotation (neutral connotations are coded as NA). With just a few lines of code, we can now tag each token as either "positive" or "negative."  

 ```r
 sentiments=get_sentiments("bing")
 bing_word_counts = tidy.token.schrute %>%
  inner_join(sentiments%>%filter(sentiment=='positive'|sentiment=='negative')) %>%
  count(word, sentiment, sort = TRUE)
 ```
<table class="image">
<tr><td><img src="word_bar.pdf" alt=" "/></td></tr>
</table>  

Yet another way to visualize this is a <b>comparative word cloud</b>.
```r
bing_word_counts %>%
  acast(word~sentiment, value.var='n', fill = 0) %>%
  comparison.cloud(colors=c("#F8766D", "#00BFC4"), 
                   max.words=100)
```
<table class="image">
<tr><td><img src="comparison_cloud.pdf" alt=" "/></td></tr>
</table>  




