import sys
import re
import hunspell

class cleanTweet:


    def __init__(self,tweet):
        self.tweet=tweet
        removeEmotion()
        replaceAtMention()
        seperateCojoinedWords()
        removeExtraSpaces()
        removeEmojis()
        correctSpelling()
        return self.tweet



    def removeEmotion(self):
        pattern=re.compile(r'::\s\w*')
        self.tweet=pattern.sub(r'',self.tweet)              #eliminating the Emotions which start with ::


    def replaceAtMention(self):
        pattern=re.compile(r'(@) (a-zA-Z0-9)+')

        matches=pattern.finditer(self.tweet)
        replacement_list=[]
        for match in matches:
            replacement_list=replacement.append((match.group(2)).upper())              #make a list corresponding to the                                      
                                                                                        #word after @                                                    														                                                           #upper case (@rohan-->ROHAN)
        for match,replacement in zip(matches,replacement_list):
            re.sub(match, '*{}*'.format(replacement), self.tweet)             #looping through the combined list made using zip   
                                                                               #function   

    def seperateCojoinedWords(self):
        patterns=re.compile(r'^\b[A-Z]')                 # capital letters not at the word boundary using \b (MyNameIsRohan)
        for pattern in patterns:
            re.sub(pattern,' {}'.format(pattern),self.tweet)      #puts a space to seperate cojoined capital letters


    def removeExtraSpaces(self):
        re.sub("\s\s+","\s",self.tweet)


    def correctSpelling:
        spellchecker=hunspell.Hunspell('/usr/share/hunspell/de_DE.dic','/usr/share/hunspell/de_DE.aff')  #creates an instance

        for word in self.tweet:
            condition=spellchecker.spell(word)          #if word does not exists, returns False
            if condition is False:
                word_replace=spellchecker.suggest(word)
                re.sub(word.word_replace,self.tweet)                #the suggested word replaces the original word


    def removeEmojis:
        pattern=re.compile(r'(-:;}{)(\[\])+')
        re.sub(pattern,'',self.tweet)


with open('jan9-2012.txt','r') as f1:
    with open('tweets_cleaned','w') as f2:

        contents=f1.read()
        tweets=contents.split('\n')

        for tweet in tweets:
            f2.write(cleanTweet(tweet) + '\n')
