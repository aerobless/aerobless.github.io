# OS X Tips & Tricks


## Shell

### Kill application on port

+ Command: `lsof -ti:port | xargs kill`
+ Example Usage: `lsof -ti:8080 | xargs kill`
