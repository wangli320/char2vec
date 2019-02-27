<center> <h1>chars2vec </h1> </center>
<center> <h4>Character-based word embeddings model based on RNN</h4> </center>


The chars2vec language model is based on the symbolic representation of words 
– the model maps each word to a vector of a fixed length. Model tries map the 
most similar words to the most closed vectors. With current approach is possible 
to create an embedding in vector space for any sequence of characters. 
Chars2vec is based on TensorFlow deep neural network so it does not keep 
dictionary of embeddings and generates vector inplace using pretrained model.  

There are pretrained models of dimensions 50, 100 and 150 for the English 
language. Library provides convenient user API to train model for arbitrary 
set of characters.  Read more details about the architecture of [Chars2vec: 
Character-based language model for handling real world texts with spelling 
errors and human slang](https://towardsdatascience.com).

<h4>Model available for Python 2.7 and 3.0+.</h4>

<center> <h3>Installation </h3> </center>

<h5> 1. Build and install from source </h5>
Download project source and run in your command line

~~~shell
>> python setup.py install
~~~

<h5> 2. Via pip </h5>
Run in your command line

~~~shell
>> pip install chars2vec
~~~

### Usage

Method `chars2vec.load_model(str model_path)` initializes the model from file.
There are three pretrained English model with dimensions: 50, 100 and 150.
To load this pretrained models:

~~~python
import chars2vec

# Load Inutition Engineering pretrained model
# Models names: 'eng_50', 'eng_100', 'eng_150'
c2v_model = chars2vec.load_model('eng_50')
~~~ 
Method `chars2vec.vectorize_words(words)` returns `numpy.ndarray` of shape `(n_words, dim)` with word embeddings.

~~~python
words = ['list', 'of', 'words']

# Create word embeddings
word_embeddings = c2v_model.vectorize_words(words)
~~~

### Training

`chars2vec.train_model` function creates and trains new chars2vec model.
The arguments of this function are the dimensionality of the model `dim`,
training dataset `training_set`, and a list of chars for the model `model_chars`.
Characters that are not in the `model_chars` list will be ignored by the model
when the text is vectorized. 

Each element of the training dataset must be represented by a pair of words
and a target value that describes the proximity of the words. 
Thus, each row of the list `training_set` should be like `*word_1* *word_2* *target_value`.
Read more about the format of the training data set and the method 
of generating in [article about chars2vec](https://towardsdatascience.com).

`chars2vec.train_model` function returns the trained model.
Save the trained model by using the function `chars2vec.save_model`.


@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@

*Создание новой модели и ее обучение выполнется функцией `chars2vec.train_model`.
В качестве аргументов этой функции требуется указать размерность модели `dim`,
набор обучающих данных `training_set` и список существенных для модели символов
`model_chars`. Символы, не входящие в список `model_chars`, 
будут игнорироваться моделью при векторизации текста.*

*Каждый элемент набора обучающих данных должен быть представлен парой слов и
целевым значением, описывающим близость написания этих слов. Таким образом, каждая 
строка из списка training_set должна иметь вид `*word_1* *word_2* *target_value*`.
Подробнее о формате обучающего набора данных и способе его генерации читайте в 
[статье](https://towardsdatascience.com).*

*Функция `chars2vec.train_model` возвращает обученную модель. 
Сохранить обученную модель можно с помощью функции `chars2vec.save_model`.*

@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@


~~~python
import chars2vec

dim = 50
path_to_model = 'path/to/model/directory'
path_to_training_set = 'path/to/txt/file/with/training/set'
training_set = open(path_to_training_set, 'r').readlines()

model_chars = ['!', '"', '#', '$', '%', '&', "'", '(', ')', '*', '+', ',', '-', '.',
               '/', '0', '1', '2', '3', '4', '5', '6', '7', '8', '9', ':', ';', '<',
               '=', '>', '?', '@', '_', 'a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i',
               'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w',
               'x', 'y', 'z']

my_c2v_model = chars2vec.train_model(dim, training_set, model_chars)
chars2vec.save_model(my_c2v_model, path_to_model)
~~~

Initialize your model by `chars2vec.load_model` function.
Specify the path to the model directory as an argument.


@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@

*Инициализации вашей модели осуществляется функцией `chars2vec.load_model`.
Укажите путь к директории модели в качестве аргумента.*
 
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@


~~~python
c2v_model = chars2vec.load_model(path_to_model)
~~~

Full code examples for usage and training models see in `example_usage.py` and `example_training.py` files.


@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@

*Полный код примеров использования и обучения модели смотри в файлах `example_usage.py` и `example_training.py`.*

@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@


<center> <h3>Contact us</h3> </center>

Website of our team [IntuitionEngineering](https://intuition.engineering).

Core developer email: v4@intuition.engineering.

Intuition dev email: dev@intuition.engineering.
