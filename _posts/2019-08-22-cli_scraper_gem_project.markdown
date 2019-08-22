---
layout: post
title:      "CLI Scraper Gem Project"
date:       2019-08-22 20:28:26 +0000
permalink:  cli_scraper_gem_project
---


The past few weeks I have been working on my CLI Scraper Project. I decided to scrape IMDB's 50 Top Rated Movies site. The scraper was quite difficult to build until I understood that I should be scraping 'movie-cards' all together rather than individually. 

One element of the project that really challenged me was getting my scraper to go down a level. I needed to initially scrape the 'movie-cards' url with the rest of the information, and then use that url to find out more information about the movie on a different webpage. 

The code below made a movie, using the variable |m| that stood for the 'movie-card' css selector:

```
  def self.new_from_index_page(m)
    title = m.css('h3 a').text
    bio = m.css('p.text-muted')[1].text.strip
    certificate = m.css('span.certificate').text.strip
    genre = m.css('span.genre').text.strip.downcase
    rating = m.css('strong').text.strip
    url = "https://imdb.com" + m.css('h3 a').attr('href') + "?ref_=adv_li_tt"
    new(title, bio, rating, certificate, genre, url)
   end
```

Then I assigned a variable name to the url being opened with open-uri 

```
def doc
    @doc ||= Nokogiri::HTML(open(self.url))
  end
```

Afterwards I could use the variable similarly to how I used m to generate my 'movie-card' above, and pulled out the different awards the movie had won from thhe page below. 

```
  def awards
    @awards ||= doc.css("span.awards-blurb b").text
  end
```

When the awards were generated with the code above I got this output: 

```
            Won
            11
            Oscars.
```

There was too much whitespace on the side, so I googled how to get rid of whitespace and got the following answer:

```
.gsub(/\s+/, " ").strip.chomp(".")
```

I added this to thhe end of my awards method and the output when I re-ran the programme was:

```
Won 11 Oscars
```


