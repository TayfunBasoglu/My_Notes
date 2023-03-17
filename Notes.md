# Nltk Nedir ?

NLTK (Natural Language Toolkit) bir doğal dil işleme (NLP) kütüphanesidir ve Python programlama dilinde kullanılabilir. NLTK, metin verileriyle çalışmak için bir dizi araç sağlar ve çeşitli NLP görevlerini gerçekleştirmek için kullanılabilir. Bu görevler arasında metin önişleme (örneğin, tokenizasyon, stop word removal), kelime dağarcığı oluşturma, konuşma tanıma, kelime öbekleme, dil modelleri, sınıflandırma, etiketleme ve sentezleme gibi işlemler yer alır.

NLTK'nin amacı, doğal dil verilerini işlemeyi kolaylaştırmak ve NLP araştırmacıları ve uygulayıcıları için bir dizi araç sağlamaktır. Bu kütüphane, öğrenme kaynakları ve kod örnekleri gibi çeşitli kaynaklara erişebilir ve doğal dil işleme konusunda birçok farklı problemi ele almak için kullanılabilir.


# Text Preprocessing

## Lower - Upper

~~~~python
input_str = "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis lobortis ante a odio varius, sed efficitur lorem scelerisque. Vivamus eu enim nunc. Vivamus ut varius purus. Donec tellus turpis, mollis ac cursus at, interdum ac ex. Mauris mattis molestie erat eget fermentum. Donec sem orci, pulvinar vitae augue sed, aliquet cursus neque. Morbi dignissim in leo sed maximus. In placerat risus scelerisque molestie pretium. Pellentesque pellentesque sem et turpis placerat condimentum. Suspendisse est ipsum, suscipit id molestie non, dapibus at lorem. Aenean eu consequat leo. Maecenas et sem sed tortor rhoncus consectetur eget vel risus. Nunc at lacus viverra, ultrices odio quis, vulputate nunc."
input_str = input_str.lower()
print(input_str)
~~~~

~~~~python
input_str = "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis lobortis ante a odio varius, sed efficitur lorem scelerisque. Vivamus eu enim nunc. Vivamus ut varius purus. Donec tellus turpis, mollis ac cursus at, interdum ac ex. Mauris mattis molestie erat eget fermentum. Donec sem orci, pulvinar vitae augue sed, aliquet cursus neque. Morbi dignissim in leo sed maximus. In placerat risus scelerisque molestie pretium. Pellentesque pellentesque sem et turpis placerat condimentum. Suspendisse est ipsum, suscipit id molestie non, dapibus at lorem. Aenean eu consequat leo. Maecenas et sem sed tortor rhoncus consectetur eget vel risus. Nunc at lacus viverra, ultrices odio quis, vulputate nunc."
input_str = input_str.upper()
print(input_str)
~~~~


## Remove Numbers

~~~~python
import re
input_str = "4 Apple and 5 dogs"
result = re.sub(r'\d+', '', input_str)
print(result)
~~~~

## Just Numbers

~~~~python
import re
input_str = "4 Apple and 5 dogs"
result = re.findall(r'\d+', input_str)
print(result)
~~~~


## Remove Punctuation

~~~~python
import string

def remove_punctuation(text):
    translator = str.maketrans('', '', string.punctuation)
    return text.translate(translator)

text = "Hello, World! $?=How are you doing today?"
text_without_punct = remove_punctuation(text)
print(text_without_punct)

~~~~


# Remove Whitespaces (Extra)

~~~~python
def remove_duplicate_whitespace(text):
    return ' '.join(text.split())

text = "   Hello,   World!   How are you doing   today?   "
text_cleaned = remove_duplicate_whitespace(text)
print(text_cleaned)
~~~~

~~~~
Hello, World! How are you doing today?
~~~~


# Left-Right Whitespaces

~~~~python
def remove_chars(text, chars):
    return text.strip(chars)

text = "   Hello, World! How are you doing today?   "
text_cleaned = remove_chars(text, " ,!")
print(text_cleaned)
~~~~























