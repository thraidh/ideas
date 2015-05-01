# Overview

This document describes a browser extension which combines local searching, tagging, bookmarking and categorization.

# Features

## Local search

- every visited page will be added to a local index
- pages will be kept in the index for a number of days or until it reaches a specified size
- pages viewed in private mode will not be added
- a local search engine can search all these indexed pages
- the search engine can be accessed from the browser
- the orginial page will be opened if one of the found pages is clicked (not the locally cached version)

## Bookmarking

- if a page is bookmarked, it is simply moved into a different index, where it won't be evicted automatically

## Categorization/Tagging

- when a page is bookmarked, the user can provide tags
- from these tags a Bayesian filter will be used to automatically tag other pages
- these tags will be presented as a default when bookmarking
- likely tags could be displayed in the location bar, so the user could easily remove wrong tags
- title words and meta tags will be preferred


