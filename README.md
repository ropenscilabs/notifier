[![Project Status: Abandoned – Initial development has started, but there has not yet been a stable, usable release; the project has been abandoned and the author(s) do not intend on continuing development.](https://www.repostatus.org/badges/latest/abandoned.svg)](https://www.repostatus.org/#abandoned)
[![Coverage Status](https://img.shields.io/codecov/c/github/ropenscilabs/ponyexpress/master.svg)](https://codecov.io/github/ropenscilabs/ponyexpress?branch=master)

ponyexpress 🐴
=============

This package builds on the `gmailr` package and code from Jenny Bryan to automate sending Gmail from R with data from a spreadsheet (local csv, Excel sheet, or a Google sheet). With nothing more than a list of names and email addresses, you can send templated emails (grades, conference acceptances etc)

Install
-------

``` r
# Obtain the the development version from GitHub:
# install.packages("devtools")
devtools::install_github("ropenscilabs/ponyexpress")
```

Functionality
-------------

-   `parcel_create(df, sender_name, sender_email, subject, template)` - Creates a template of the messages that need to be sent.
-   `parcel_preview()` - will preview the emails
-   `parcel_send()` - Send the emails

![](http://rs181.pbsrc.com/albums/x148/brandi47_2007/4942733.gif~c200)

Example
-------

**1. Read in data frame**

``` r
 df <- data.frame(
    name = c("Lucy", "Karthik"),
    email = c("ld.mcgowan@vanderbilt.edu", "kram@berkeley.edu")
  )
  df
```

    ##      name                     email
    ## 1    Lucy ld.mcgowan@vanderbilt.edu
    ## 2 Karthik         kram@berkeley.edu

**2. Template up**

``` r
library(ponyexpress)
template <- "Dear {name},

   This is a friendly email from me.

  XO,
   Lucy"

 # Or write a rich template!

rich_template <- "Dear {name},

   This is a friendly email from me.
  \\<img src='http://bukk.it/wut.jpg'>
   XO,
   Lucy"
 
 # Or use one of our templates!
 # Save your text as an object named "body"
 # then use glue!
body <- "Dear {name},

   This is a friendly email from me.
  \\<img src='http://bukk.it/wut.jpg'>
   XO,
   Lucy"
our_template <- glue::glue(glitter_template)
```

**3. Parcel & Preview**

``` r
  parcel <- parcel_create(df,
              sender_name = "Lucy",
              sender_email = "lucydagostino@gmail.com",
              subject = "Happy email!",
              template = rich_template)

 parcel_preview(parcel)            
```

**4. Send**

``` r
parcel_send(parcel)
```

![](https://i.imgur.com/Ij60FhR.gif)

![](ponies.png)
