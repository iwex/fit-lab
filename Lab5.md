Код:
```r
> url <- read_html("http://www.imdb.com/search/title?count=100&release_date=2017,2017&title_type=feature")
> html <- html_nodes(url,'.text-primary')
> data <- html_text(html)
> data <- as.numeric(data)
> title_html <- html_nodes(url,'.lister-item-header a')
> title <- html_text(title_html)
> runtime_html <- html_nodes(url,'.text-muted .runtime')
> runtime <- html_text(runtime_html)
> runtime <- gsub(" min", "", runtime)
> runtime <- as.numeric(runtime)
> movies <- data.frame(Rank = data, Title = title, Runtime = runtime, stringsAsFactors = FALSE )
```

1.	Виведіть перші 6 назв фільмів дата фрейму.
```r
> head(movies$Title, 6)
[1] "Зорянi вiйни: Останнi Джедаi"   "The Disaster Artist"            "The Shape of Water"             "Лiга справедливостi"           
[5] "Jumanji: Welcome to the Jungle" "Тор: Рагнарок"      
```

2.	Виведіть всі назви фільмів с тривалістю більше 120 хв.
```r
> movies[movies$Runtime > 120, ]$Title
 [1] "Зорянi вiйни: Останнi Джедаi"             "The Shape of Water"                       "Тор: Рагнарок"                           
 [4] "Mother!"                                  "Kingsman: Золоте кiльце"                  "Вартовi Галактики 2"                     
 [7] "Воно"                                     "The Killing of a Sacred Deer"             "Darkest Hour"                            
[10] "Call Me by Your Name"                     "Той, хто бiжить по лезу 2049"             "Валерiан i мiсто тисячi планет"          
[13] "Логан: Росомаха"                          "Phantom Thread"                           "Downsizing"                              
[16] "Диво-Жiнка"                               "Людина-павук: Повернення додому"          "Detroit"                                 
[19] "All the Money in the World"               "Molly's Game"                             "Сiм сестер"                              
[22] "Красуня i Чудовисько"                     "Вiйна за планету мавп"                    "Mudbound"                                
[25] "The Square"                               "Roman J. Israel, Esq."                    "Пiрати Карибського моря: Помста Салазара"
[28] "Трансформери: Останнiй лицар"             "Пострiл в безодню"                        "Power Rangers"                           
[31] "Hostiles"                                 "Girls Trip"                               "Джон Уiк 2"                              

```

3.	Скільки фільмів мають тривалість менше 100 хв.
```r
> length(movies[movies$Runtime < 100, ]$Title)
[1] 20
```
