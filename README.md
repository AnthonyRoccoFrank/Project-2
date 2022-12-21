# ETL Project
![etl-banner](https://user-images.githubusercontent.com/112406455/208813188-2240650d-5eda-4154-8488-7afc62f3519f.jpg)
## Introduction
The purpose of this ETL project was to analyze two datasets containing information about music artist and the use of profanity in their lyrics. In addition to these datasets, we also used web scraping techniques to gather information about the top 50 best selling albums of all time. The first dataset contained information about the artists' songs and lyrics, while the second dataset contained information about the artist genres and popularity score. By merging and analyzing these datasets, we were able to identify which genres had the highest use of profanity, which artists were the most popular based on search data, and which albums had the highest sales. The merged datasets were then stored in a MongoDB database. The resulting insights can provide valuable information for music industry professionals and researchers interested in understanding trends in language use, artist popularity, and album sales. 
## Data Sources
The two datasets we used for the project are csv files that were obtained from Kaggle which were orginally sourced by scraping the Brazilian website [Vagalume](https://www.vagalume.com.br/). 
* The lyrics-data.csv has five columns:
  * Alink: Link to the artist profile in Vagalume.com
  * SName: Song's Name
  * Slink: Link to the song lyrics in Vagalume.com
  * Lyric: Song lyrics
  * language: Lyrics' language
* The artists-data.csv has five columns:
  * Artist: Artist name
  * Genres: Musical styles
  * Songs: Number of songs the arist has
  * Popularity: Popularity score based on how much each artist/lyric is accessed on the website
  * Link: Link to the artist profile in Vagalume.com 
## ETL Process

## Output
## Usage
## Limitations and Future Work
## Conclusion
## Additional Resources
