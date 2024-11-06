
## project_5 
 
# Представим, что некое приложение хранит плейлист песен в двух видах: 
#   * многострочная строка 
#   * кортеж из двух словарей 
# Каждая песня содержит: название и время звучания. 
 
# Задание 
# 1. Посчитайте общее время звучания n случайных песен, где n - количество запрошенных песен 
# 2. Используйте модули random и datetime. Или любые другие. 
# 3. Решение должно включать функцию, которая в качестве аргумента способна принимать плейлисты разных типов данных 
 
# В результате решением задачи является функция, которая: 
#   * может принимать как первый плейлист, так и второй в качестве аргумента 
#   * принимает параметр n, число. Это количество песен 
#   * возвращает время звучания, как объект времени timedelta, либо строку, либо вещественное число 
# При этом функций в задаче может быть несколько. То есть решение можно разбить на несколько функций. 
# Но результат задачи можно получить вызвав одну функцию! 
# get_duration(playlist: Iterable, n: int) -> Any 


import random
import re

# Функция для парсинга плейлиста строк
def parse_playlist_e(playlist):
    pattern = re.compile(r"(.+?)\s+(\d+[\.:]\d+)")
    songs = pattern.findall(playlist)
    return {name: float(time.replace(':', '.')) for name, time in songs if time}

# Функция для парсинга плейлиста из кортежа 
def parse_playlist_f(playlist):
    combined_dict = {}
    for p in playlist:
        combined_dict.update(p)
    return combined_dict


# Функция для объединения двух плейлистов
def combine_playlists(playlist_e, playlist_f):
    playlist_e_dict = parse_playlist_e(playlist_e)
    playlist_f_dict = parse_playlist_f(playlist_f)
    combined_playlist = {**playlist_e_dict, **playlist_f_dict}
    return combined_playlist


