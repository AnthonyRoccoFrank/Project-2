# ETL Project
![etl-banner](https://user-images.githubusercontent.com/112406455/208813188-2240650d-5eda-4154-8488-7afc62f3519f.jpg)
## Introduction
The purpose of this ETL project was to analyze two datasets containing information about music artist and the use of profanity in their lyrics. In addition to these datasets, we also used web scraping techniques to gather information about the top 50 best selling albums of all time. The first dataset contained information about the artists' songs and lyrics, while the second dataset contained information about the artist genres and popularity score. By merging and analyzing these datasets, we were able to identify which genres had the highest use of profanity, which artists were the most popular based on search data, and which albums had the highest sales. The merged datasets were then stored in a MongoDB database. The resulting insights can provide valuable information for music industry professionals and researchers interested in understanding trends in language use, artist popularity, and album sales. 
## Data Sources
The two datasets we used for the project are csv files that were obtained from Kaggle which were orginally sourced by scraping the Brazilian website [Vagalume](https://www.vagalume.com.br/). 
* The [lyrics-data.csv](https://www.kaggle.com/datasets/neisse/scrapped-lyrics-from-6-genres?select=lyrics-data.csv) has five columns:
  * Alink: Link to the artist profile in Vagalume.com
  * SName: Song's Name
  * Slink: Link to the song lyrics in Vagalume.com
  * Lyric: Song lyrics
  * language: Lyrics' language
* The [artists-data.csv](https://www.kaggle.com/datasets/neisse/scrapped-lyrics-from-6-genres) has five columns:
  * Artist: Artist name
  * Genres: Musical styles
  * Songs: Number of songs the arist has
  * Popularity: Popularity score based on how much each artist/lyric is accessed on the website
  * Link: Link to the artist profile in Vagalume.com 
## ETL Process
The following steps were taken to extract, transform, and load the data:

1. First we imported all dependencies
 <img width="1010" alt="Screenshot 2022-12-21 at 6 56 21 PM" src="https://user-images.githubusercontent.com/112406455/209032213-48471913-e086-4951-940c-c375d41baf8a.png">

2. The `artists` and `lyrics` data sets were read in from `.csv` files.
<img width="1011" alt="Screenshot 2022-12-21 at 7 03 20 PM" src="https://user-images.githubusercontent.com/112406455/209032548-9cb86c1c-9a44-4d78-ba05-b18785117b87.png">

3. The `ALink` column in the `lyrics` data set was renamed to `Link`.
<img width="1011" alt="Screenshot 2022-12-21 at 7 08 12 PM" src="https://user-images.githubusercontent.com/112406455/209033169-a8a8c287-bee5-4f80-b100-8ebbb6bfd98b.png">

4. The `artists` and `lyrics` data sets were merged on the `Link` column.
<img width="1012" alt="Screenshot 2022-12-21 at 7 13 15 PM" src="https://user-images.githubusercontent.com/112406455/209033490-e5adf0e3-cf1d-499c-9425-7d8eefb02d92.png">

5. Unnecessary columns were dropped from the merged data set.
<img width="1011" alt="Screenshot 2022-12-21 at 7 23 54 PM" src="https://user-images.githubusercontent.com/112406455/209034595-ff054fa5-ca9f-4678-b6f4-a0fe8039b01b.png">

6. The `SName` column in the merged data set was renamed to `Song Title`.
<img width="1012" alt="Screenshot 2022-12-21 at 7 27 47 PM" src="https://user-images.githubusercontent.com/112406455/209035042-b68dc641-af20-462d-913e-2cde2e2caff0.png">

7. Subsets of the data set were created based on the value of the `Artist` column (for `taylor_swift`) and the `language` column (for `english_songs`).
<img width="1009" alt="Screenshot 2022-12-21 at 7 31 41 PM" src="https://user-images.githubusercontent.com/112406455/209035522-da4d5457-0097-4b70-9850-55876a11c5d0.png">
<img width="1010" alt="Screenshot 2022-12-21 at 7 31 50 PM" src="https://user-images.githubusercontent.com/112406455/209035578-60575064-07f4-4a01-975c-39b4198462d2.png">

8. The number of instances of certain explicit words in the `Lyric` column of the `english_songs` data set were counted.
<img width="1011" alt="Screenshot 2022-12-21 at 7 40 02 PM" src="https://user-images.githubusercontent.com/112406455/209036315-82a31995-9d16-4974-bd06-eeb0184a0bdc.png">

9. Subsets of the data set were created based on the value of the `Genres` column, for various music genres.
<img width="1011" alt="Screenshot 2022-12-21 at 7 46 51 PM" src="https://user-images.githubusercontent.com/112406455/209037027-9cc23fd6-d5ed-4ef6-bb06-26a61b109db4.png">

10. The number of instances of certain explicit words in the `Lyric` column of each genre-specific data set were counted.
<img width="1012" alt="Screenshot 2022-12-21 at 7 50 52 PM" src="https://user-images.githubusercontent.com/112406455/209037509-f8ab1c9f-6a57-4ba2-ae8e-5ac6566df9b4.png">

11. A new data frame, `profanity_counts`, was created with the genre names and explicit word counts.
<img width="1264" alt="Screenshot 2022-12-21 at 7 52 10 PM" src="https://user-images.githubusercontent.com/112406455/209037776-2e471ad1-7f6e-44cc-857b-81d8a85eeee0.png">

12. Set up a `Browser` object using the `chrome` driver and `ChromeDriverManager`.
<img width="1011" alt="Screenshot 2022-12-21 at 8 15 00 PM" src="https://user-images.githubusercontent.com/112406455/209040494-6519a2ec-7b3c-4617-973c-0f388af1a2c2.png">

13. Specify the URL of the web page to be scraped and send an HTTP request to the specified URL using the `visit()` method of the `Browser` object.
<img width="1014" alt="Screenshot 2022-12-21 at 8 10 28 PM" src="https://user-images.githubusercontent.com/112406455/209040613-672af80c-2898-4c5e-9f29-5b81085b9f8d.png">

14. Parse the HTML of the web page using `BeautifulSoup` and extract the desired data from the web page by finding all the `div`elements with the class `album_card` and using the `find()` method to extract the rank, title, artist, and sales data for each album. Clean and transform the data as needed, such as removing unnecessary characters from the sales data and converting it to an integer. Store the data in a dictionary and a list. Write the data to a `.csv` file using the `csv` library.
<img width="1013" alt="Screenshot 2022-12-21 at 8 13 55 PM" src="https://user-images.githubusercontent.com/112406455/209041284-2a1e1b1e-84c9-4e66-a5c1-7bc44bc55107.png">

15. Load in the csv file
<img width="1012" alt="Screenshot 2022-12-21 at 8 27 49 PM" src="https://user-images.githubusercontent.com/112406455/209042111-dfc26b1b-14fa-4f22-8573-940503206000.png">

16. Then capitalize the `Artist` column in the `new_df` dataframe using the `.str.upper()` method so it can be merged with the `bestsellers_df`
<img width="1012" alt="Screenshot 2022-12-21 at 8 27 56 PM" src="https://user-images.githubusercontent.com/112406455/209042599-f04cb5b7-77b3-4eb9-bb84-4f4982226f68.png">

17. Group the data by artist and sum the sales for each artist using the `groupby()` and `sum()` methods of the data frame, creating a new data frame.
<img width="1009" alt="Screenshot 2022-12-21 at 8 35 17 PM" src="https://user-images.githubusercontent.com/112406455/209042970-54084a0c-3485-47f5-91bf-2a56ae0b853d.png">

18. Merge the original data set with the new data frame using the `pd.merge()` function, specifying the relevant columns or indices to join on.
<img width="1009" alt="Screenshot 2022-12-21 at 8 37 17 PM" src="https://user-images.githubusercontent.com/112406455/209043133-2c17ff67-fc7e-4cd6-bab5-a585f4324eb6.png">

## Output
## Usage
## Limitations and Future Work
## Conclusion
## Additional Resources
