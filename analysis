import pickle

#A1 
def read_text(text_path):
    '''
    str -> lst<str>
    
    Returns a list of all the comments inside the file after removing
    user pseudonym,

    Examples:
    >>> reads_text("text.txt")
    ['Hello \n', 'How are you today? \n', 'Good I hope! \n', 'ok take care! \n'] 
    
    '''
    try: 
        comments = open(text_path, 'r')
        
        #to collect comments 
        text= ''
        text_list = []
    
        for user in comments: 
            for i in range(len(user)):
                if user[i] == ',':
                    
                    #slice away user psedeudoynm
                    text += user[i+1:]
                    text_list += [text]
                    
                    #restart to collect new comment
                    text = ''
                    
        comments.close()

        return text_list

    except FileNotFoundError:
        print("File does not exist")
    
#A2
def read_pickle(path_to_pkl):
    '''
    str -> dict<str>
    
    Returns content of a pickle file containing dictionaries
    
    Examples:
    >>> read_pickle('sentiment_dictionary.pkl')
    {'POSITIVE': ['great', 'love', 'recommend', 'laugh', 'happy', 'brilliant'],
    'NEGATIVE': ['terrible', 'awful', 'hideous', 'sad', 'cry', 'bad'],
    'NEUTRAL': ['meh', 'indifferent', 'ignore']}
    '''
    file_dict = open(path_to_pkl,'rb')
    
    word_dict = pickle.load(file_dict)
    
    file_dict.close()
    
    return word_dict

#A3
def sentiment_frequencies(text, dictionary_word):
    '''
    (str, dict<str>) -> dict<int>
    
    Returns the frenquency of each sentiment that appears in the text
    
    Examples:
    >>> dic = {'POSITIVE':['great','love','recommend','laugh','happy','brilliant'], 'NEGATIVE':['terrible','awful','hideous','sad','cry','bad'], 'NEUTRAL':['meh', 'indifferent','ignore']} 
    >>> text = 'i love this movie it is great and the adventure scenes are fun i highly recommend it but the theatre was terrible and there was an awful smell'
    >>> sentiment_frequencies(text, dic)
    {'POSITIVE': 0.11, 'NEGATIVE': 0.07, 'NEUTRAL': 0.0}
    
    >>> dic = {'POSITIVE':['great','love','recommend','laugh','happy','brilliant'], 'NEGATIVE':['terrible','awful','hideous','sad','cry','bad'], 'NEUTRAL':['meh', 'indifferent','ignore']} 
    >>> text = 'this cafe is awful and the food is hideous the atmosphere was happy but the location was meh and indifferent'
    >>> sentiment_frequencies(text, dic)
    {'POSITIVE': 0.05, 'NEGATIVE': 0.1, 'NEUTRAL': 0.1}

    >>> dic = {'POSITIVE':['great','love','recommend','laugh','happy','brilliant'], 'NEGATIVE':['terrible','awful','hideous','sad','cry','bad'], 'NEUTRAL':['meh', 'indifferent','ignore']} 
    >>> text = 'i love this place'
    >>> sentiment_frequencies(text, dic)
    {'POSITIVE': 0.25, 'NEGATIVE': 0.0, 'NEUTRAL': 0.0}
    '''
    
    text = text.lower()
    
    list_text = text.split(' ')     

    dict_frequency = {'POSITIVE': 0, 'NEGATIVE': 0, 'NEUTRAL': 0}
   
    list_sent = []
    
    #collect sentimental words
    for word in list_text:
        if (word in (dictionary_word['POSITIVE']) or  word in
        (dictionary_word['NEGATIVE']) or word in (dictionary_word['NEUTRAL'])): 
            list_sent += [word]
    
    #count occurance of each sentimental category
    for word in list_sent:
        if word in dictionary_word['POSITIVE']:
            dict_frequency['POSITIVE'] += 1
            
        elif word in dictionary_word['NEGATIVE']:
            dict_frequency['NEGATIVE'] += 1
    
        else:
            dict_frequency['NEUTRAL'] += 1

    #calculate frequencies
    word_count = len(list_text)
    for key in dict_frequency:
        dict_frequency[key] = round(((dict_frequency[key] / word_count)), 2)
    
    return dict_frequency

#A4
def compute_polarity(dict_frequency):
    '''
    dict<int> -> str
    
    Returns the most occuring sentiment catergory either,
    POSITIVE, NEGATIVE or NEUTRAL
    
    Examples:
    >>> d = {'POSITIVE': 0.11, 'NEGATIVE': 0.07, 'NEUTRAL': 0.0}
    >>> compute_polarity(d)
    'POSITIVE'
    
    >>> d = {'POSITIVE': 0.0, 'NEGATIVE': 0.11, 'NEUTRAL': 0.20}
    >>> compute_polarity(d)
    'NEUTRAL'
    
    >>> d = {'POSITIVE': 0.0, 'NEGATIVE': 0.30, 'NEUTRAL': 0.30}
    >>> compute_polarity(d)
    'NEGATIVE'
    
    '''
    highest_freq = 0 
    
    polarity = ''
    
    for key in dict_frequency:
        if dict_frequency[key] > highest_freq:
            highest_freq = dict_frequency[key]
            polarity = key
            
    return polarity 

#A5
def analyse_text(text_path, dict_path):
    '''
    (str, dict<str>) -> lst<str>
    
    Return a list of polarity of each line in the text file
    
    text.txt = user1,Hello\nuser2,How are you today?\nuser3,Good I hope!
    user4,ok take care! 
    
    example.txt = ashraqattem, love the cafe/nareebaxahmed, yup i recommend it
    
    Examples:
     >>> analyse_text('posts.txt','sentiment_dictionary.pkl')
    ['POSITIVE', 'NEGATIVE', 'NEUTRAL', 'POSITIVE']
    
    >>> analyse_text('text.txt','sentiment_dictionary.pkl')
    ['', '', '', '']
    
    >>> analyse_text('example.txt','sentiment_dictionary.pkl')
    ['POSITIVE', 'POSITIVE']
    '''
    list_polarity = []
    stop_words = ['!','.','?',';','\n']
    
    text_list = read_text(text_path)
    
    dict_pickle = read_pickle(dict_path)
    
    for line in text_list:
        line = line.strip()
        line = line.lower()

        for symbol in stop_words:
            if symbol in line:
                line = line.replace(symbol,'')
        
        line_frequency = sentiment_frequencies(line, dict_pickle)
        
        line_polarity = compute_polarity(line_frequency)
        
        list_polarity += [line_polarity]
    
    return list_polarity 



        
    
            
          
           
