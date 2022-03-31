____
### Download videos from youtube using a list of links

```
youtube-dl -c -f best --batch-file youtube_downloadlist.txt -o "%(title)s-%(id)s.%(ext)s" --restrict-filenames

#-o "%(title)s-%(id)s.%(ext)s" -> replaces deprecated --title 
#-f best -> use the best available format
#--restrict-filenames -> replace space and & in filenames 
#-c -> force resume of partially downloaded files
```
___
