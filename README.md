# Codesofttask3-AI
import numpy as np


ratings = np.array([
    [5, 4, 0, 0, 2, 1],
    [0, 0, 4, 5, 0, 3],
    [2, 0, 1, 0, 4, 0],
    [0, 2, 0, 0, 5, 4]
])

def recommend_movies(ratings, user_index, num_recommendations=3):
   
    user_similarities = np.dot(ratings, ratings[user_index]) / (np.linalg.norm(ratings, axis=1) * np.linalg.norm(ratings[user_index]))
    

    similar_users = np.argsort(user_similarities)[::-1]
    
    
    unrated_movies = np.where(ratings[user_index] == 0)[0]
    recommended_movies = []
    for movie_index in unrated_movies:
        movie_ratings = ratings[similar_users, movie_index]
        avg_rating = np.mean(movie_ratings[movie_ratings > 0])
        recommended_movies.append((movie_index, avg_rating))
    
   
    recommended_movies.sort(key=lambda x: x[1], reverse=True)
    
    return [movie[0] for movie in recommended_movies[:num_recommendations]]


user_index = 0
recommended_movie_indices = recommend_movies(ratings, user_index)

print("Recommended movie indices:", recommended_movie_indices)
