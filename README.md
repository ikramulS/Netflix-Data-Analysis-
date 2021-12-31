# Netflix-Data-Analysis-
Netflix! What started in 1997 as a DVD rental service has since exploded into the largest entertainment/media company by market capitalization, boasting over 200 million subscribers as of January 2021.
Given the large number of movies and series available on the platform, it is a perfect opportunity to flex our data manipulation skills and dive into the entertainment industry. Our friend has also been brushing up on their Python skills and has taken a first crack at a CSV file containing Netflix data. For their first order of business, they have been performing some analyses, and they believe that the average duration of movies has been declining. We are going to inspect that.

years = [2011,2012,2013,2014,2015,2016,2017,2018,2019,2020]

durations = [103, 101, 99, 100, 100, 95, 95, 96, 93,90]

movie_dict = dict(years=years,durations=durations)

print(movie_dict)

import pandas as pd

durations_df = pd.DataFrame(movie_dict)

print(durations_df)

import matplotlib.pyplot as plt

fig = plt.figure()

plt.plot(durations_df['years'],durations_df['durations'])

plt.title('Netflix Movie Durations 2011-2020')

plt.show()

netflix_df = pd.read_csv('datasets/netflix_data.csv')

print(netflix_df.head(5))

netflix_df_movies_only = netflix_df[netflix_df['type']=='Movie']

netflix_movies_col_subset = netflix_df_movies_only[['title','country','genre','release_year','duration']]

print(netflix_movies_col_subset.head(5))

fig = plt.figure(figsize=(12,8))

plt.scatter(x=netflix_movies_col_subset['release_year'],y=netflix_movies_col_subset['duration'])

plt.title('Movie Duration by Year of Release')

plt.show()

short_movies = netflix_movies_col_subset[netflix_movies_col_subset['duration'] < 60] #.sort_values('genre',ascending=True)

print(short_movies[0:20])

colors = [] 

for lab, row in netflix_movies_col_subset.iterrows() :

   if row['genre']=="Children" :     #lab is for the row index and genre for the col , another way netflix_movies_col_subset.loc[lab,'genre'] 
   
       colors.append("red")
       
   elif row['genre']=="Documentaries" :
   
       colors.append("blue")
       
   elif row['genre']=="Stand-Up" :
   
       colors.append("green")
       
   else:
   
       colors.append("black")
          
print(colors[0:10])

plt.style.use('fivethirtyeight')

fig = plt.figure(figsize=(12,8)

plt.scatter(x=netflix_movies_col_subset['release_year'],y=netflix_movies_col_subset['duration'],c=colors)

plt.title("Movie duration by year of release")

plt.xlabel("Release year")

plt.ylabel("Duration (min)")

plt.show()



