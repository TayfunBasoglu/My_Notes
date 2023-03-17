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


## Remove Whitespaces (Extra)

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


## Left-Right Whitespaces

~~~~python
def remove_chars(text, chars):
    return text.strip(chars)

text = "   Hello, World! How are you doing today?   "
text_cleaned = remove_chars(text, " ,!")
print(text_cleaned)
~~~~



## Stop Words

Dilde sık kullanılan, ancak analiz sırasında anlamsal olarak önemsiz olan kelimelerdir. Örnek olarak İngilizce'deki "the", "a", "an", "and", "in", "on" gibi kelimeler verilebilir.

Stopwords, bir metnin boyutunu azaltmak, işlem zamanını azaltmak ve daha net sonuçlar elde etmek için metinden çıkarılabilir. Ancak, bazı NLP görevleri, özellikle duygu analizi veya sosyal medya analizi gibi görevlerde stopwords'ların önemli olduğu durumlar vardır. Bu nedenle, stopwords kullanılıp kullanılmayacağına karar vermek, analiz yapılacak metne ve kullanılacak NLP tekniklerine bağlıdır.

~~~~
import nltk
from nltk.corpus import stopwords
from nltk.tokenize import word_tokenize
import nltk
nltk.download('punkt')

text = "Merhaba, bugün güzel bir gün ama garip. Hava harika ve dışarıda yürüyüş yapmak istiyorum."
text = text.lower()

# Stopwords List
stop_words = set(stopwords.words("turkish"))

# Split
words = word_tokenize(text)

# Remove Stopwords
filtered_words = [word for word in words if word not in stop_words]

# Join and print
filtered_text = ' '.join(filtered_words)
print(filtered_text)
~~~~

~~~~
merhaba , bugün güzel bir gün garip . hava harika dışarıda yürüyüş yapmak istiyorum .
~~~~




## Stemming

Stemming, doğal dil işleme (NLP) için yapılan bir ön işleme adımıdır ve kelime köklerini bulmak için kullanılır. Özellikle metin sınıflandırması, bilgi alımı, indeksleme gibi NLP uygulamalarında sıklıkla kullanılır.

Stemming, bir kelimenin çekim eklerini kaldırarak kelimenin kök halini bulmaya çalışır. Örneğin, "played", "playing" ve "plays" kelimelerinin hepsi "play" kelimesinin köküdür. Bu nedenle stemming, bir kelimenin farklı çekim formlarını aynı kelime olarak kabul ederek, kelime sayısını azaltır ve analiz sürecini hızlandırır.

Stemming, bir kelimeyi kök haline getirirken, kelime yapısından yola çıkarak kelimeyi kesme yöntemidir. Yani kelimenin eklerini atarak kök haline getirir. Bu nedenle, stemming yöntemi daha basit ve hızlıdır, ancak kesin sonuçlar vermez. Örneğin, "koşuyor", "koştu" ve "koşacağız" kelimeleri "koş" köküne indirgenir. Bu, bazı durumlarda kelimenin anlamının bozulmasına neden olabilir.

~~~~python
from nltk.stem import PorterStemmer
from nltk.tokenize import word_tokenize

porter = PorterStemmer()

text = "I am playing with playing games"

# tokenize the text
words = word_tokenize(text)

for word in words:
    # apply stemming to each word
    print(porter.stem(word))
~~~~

~~~~
i
am
play
with
play
game
~~~~


**Türkçe**

~~~~python
from snowballstemmer import stemmer

kokbul1 = stemmer('turkish')

print(kokbul1.stemWords('vardır var'.split()))
print(kokbul1.stemWords('bildirgeyi bildirgede'.split()))
print(kokbul1.stemWords('herkes herkesin'.split()))
~~~~

~~~~
'var', 'var']
['bildirge', 'bildirge']
['herkes', 'herke']
~~~~


## Lemmatization

Lemmatization, doğal dil işleme (NLP) alanında kullanılan bir yöntemdir. Amacı, bir kelimeyi kelimenin köküne veya lemmasına dönüştürmektir. Bu, bir kelimenin farklı şekillerini tek bir temsilciyle eşleştirmeye ve daha doğru bir analiz yapmaya olanak tanır.

Örneğin, "koşuyor", "koştu", "koşacak" ve "koşmak" kelimesi "koşmak" kelimesinin farklı şekilleridir. Ancak, hepsinin temel anlamı aynıdır. Lemmatization, bu kelimeleri "koşmak" kelimesine dönüştürerek aynı temsilciyle eşleştirmeyi sağlar.

Lemmatization, stemming ile karıştırılmamalıdır. Stemming, kelimenin kökünü bulmak için hepsini keser ve lemmasına göre daha basit bir yöntemdir. Lemmatization ise, dilbilgisi kurallarını kullanarak kelimenin lemmasına dönüştürür ve bu nedenle daha karmaşık bir işlemdir.

Lemmatization, kelimenin morfolojik analizini yaparak kelimenin temel anlamını korur. Bu nedenle, lemmatization daha karmaşık ve yavaştır, ancak daha doğru sonuçlar verir. Kelimenin dilbilgisi yapılarını analiz ederek, kelimenin sözlükteki temel haline yani lemma haline dönüştürür. Örneğin, "koşuyor", "koştu" ve "koşacağız" kelimeleri "koşmak" kelimesine dönüştürülür. Bu, kelimenin anlamını koruyarak daha doğru sonuçlar elde edilmesini sağlar.
Lemmatization, kelimenin morfolojik analizini yaparak kelimenin temel anlamını korur. Bu nedenle, lemmatization daha karmaşık ve yavaştır, ancak daha doğru sonuçlar verir. Kelimenin dilbilgisi yapılarını analiz ederek, kelimenin sözlükteki temel haline yani lemma haline dönüştürür. Örneğin, "koşuyor", "koştu" ve "koşacağız" kelimeleri "koşmak" kelimesine dönüştürülür. Bu, kelimenin anlamını koruyarak daha doğru sonuçlar elde edilmesini sağlar.

~~~~python
import nltk
from nltk.stem import WordNetLemmatizer

nltk.download('wordnet')

lemmatizer = WordNetLemmatizer()

words = ['cats', 'dogs', 'horses', 'wolves', 'children', 'men', 'women']

for word in words:
    print(f"{word} -> {lemmatizer.lemmatize(word)}")
~~~~

~~~~
cats -> cat
dogs -> dog
horses -> horse
wolves -> wolf
children -> child
men -> men
women -> woman
~~~~




## Part of speech tagging

Part of speech tagging, doğal dil işleme (NLP) alanında, bir cümledeki her kelimenin dilbilgisel olarak hangi gruba ait olduğunu belirlemek için kullanılan bir tekniktir. Bu gruplar, isim, sıfat, zarf, fiil, edat, bağlaç, ünlem gibi dilbilgisel yapılar olabilir.

Part of speech tagging, kelimenin anlamını ve cümlenin yapısını anlamak için önemlidir. Örneğin, "kitap okuyorum" cümlesinde "kitap" kelimesi isim, "okuyorum" kelimesi ise fiil olarak etiketlenebilir. Bu etiketleme işlemi, dilbilgisel analiz için bir ön işlemdir ve çeşitli NLP uygulamalarında kullanılır.

Pek çok kütüphane örneği var. ( NLTK, spaCy, TextBlob, Pattern, Stanford CoreNLP, Memory-Based Shallow Parser (MBSP), Apache OpenNLP, Apache Lucene, General Architecture for Text Engineering (GATE), FreeLing, Illinois Part of Speech Tagger, and DKPro Core.)


~~~~python
import nltk

nltk.download('punkt')
nltk.download('averaged_perceptron_tagger')

sentence = "I am learning natural language processing with Python"

tokens = nltk.word_tokenize(sentence)
tagged = nltk.pos_tag(tokens)

print(tagged)
~~~~

~~~~
[('I', 'PRP'),
('am', 'VBP'),
('learning', 'VBG'),
('natural', 'JJ'),
('language', 'NN'),
('processing', 'NN'),
('with', 'IN'),
('Python', 'NNP')]
~~~~

* CC: Bağlaç (örneğin, "and", "but", "or")
* CD: Sayı (örneğin, "one", "two", "three")
* DT: Belirteç (örneğin, "the", "this", "that")
* EX: Belirteç (örneğin, "there")
* FW: Yabancı kelime
* IN: Edat (örneğin, "in", "on", "at")
* JJ: Sıfat (örneğin, "big", "happy", "red")
* JJR: Sıfat, karşılaştırma (örneğin, "bigger", "more interesting")
* JJS: Sıfat, en üstlük (örneğin, "biggest", "most interesting")
* LS: Liste işareti (örneğin, "1)", "2)", "3)")
* MD: Yardımcı fiil (örneğin, "can", "may", "should")
* NN: İsim, tekil (örneğin, "dog", "book", "city")
* NNS: İsim, çoğul (örneğin, "dogs", "books", "cities")
* NNP: İsim, tekil ve özel ad (örneğin, "John", "London", "Python")
* NNPS: İsim, çoğul ve özel ad (örneğin, "Smiths", "Mycroft Holmes")
* PDT: Ön belirleyici (örneğin, "all", "both", "many")
* POS: İşaret fiili (örneğin, "'s", "s'")
* PRP: Zamir (örneğin, "I", "you", "he/she/it", "we", "they")
* PRP$: İşaret zamiri, sahip (örneğin, "my", "your", "his/her/its", "our", "their")
* RB: Zarf (örneğin, "quickly", "very", "often")
* RBR: Zarf, karşılaştırma (örneğin, "faster", "more quickly")
* RBS: Zarf, en üstlük (örneğin, "fastest", "most quickly")
* RP: Sonek (örneğin, "up", "off", "out")
* SYM: Sembol (örneğin, "+", "-", "$")
* TO: Belirleyici (örneğin, "to")
* UH: Ünlemler (örneğin, "oh", "wow", "ouch")
* VB: Fiil, taban formu (örneğin, "run", "eat", "write")
* VBD: Fiil, geçmiş zaman (örneğin, "ran", "ate", "wrote")
* VBG: Fiil, şimdiki zaman, -ing ekli (örneğin, "running", "eating", "writing")
* VBN: Fiil, sıfat fiil, geçmiş zaman (örneğin, "run", "eaten", "written")
* WDT: Belirleyici zamir (örneğin, "which", "that")
* WP: Soru zamiri (örneğin, "who", "what", "which")
* WP$: Soru zamiri, sahip (örneğin, "whose")
* WRB: Soru zarfı (örneğin, "when", "where", "why")




## Chunking

Kelimeleri veya kelimelerin gruplarını, anlamsal olarak bir arada olan ve belirli bir yapı oluşturan parçalara (chunk) ayırma işlemidir. Bu parçalar genellikle "kelime öbekleri" veya "cümle öbekleri" olarak adlandırılır ve daha büyük bir metnin anlamını daha kolay anlaşılabilir ve yorumlanabilir parçalara böler.
 
Chunking, genellikle bir ön işleme adımı olarak kullanılır ve diğer doğal dil işleme teknikleriyle birlikte kullanılır. Bu teknik, dilbilgisi kuralları, kelime öbekleri, POS (kelime türü) etiketleri ve diğer özellikler gibi belirli öğeleri dikkate alarak cümleyi küçük parçalara ayırır. Bu sayede, cümlelerin anlamsal yapıları daha net bir şekilde ortaya çıkar ve daha doğru bir şekilde analiz edilebilir. Chunking, özellikle bilgi çıkarma, metin sınıflandırma ve duyum analizi gibi uygulamalarda sıklıkla kullanılır.

~~~~python
import nltk

# Örnek metni tanımla
text = "I have a dog named Max. He is a black Labrador Retriever. Max loves to play fetch with his tennis ball."

# Metni kelimelere ayır
tokens = nltk.word_tokenize(text)

# Kelimelerin her birine POS etiketi ata
tagged_tokens = nltk.pos_tag(tokens)

# Chunking işlemi için bir grammar tanımla
grammar = r"""
    NP: {<DT>?<JJ>*<NN>}  # Belirteç, sıfatlar ve isimden oluşan bir NP
    VP: {<MD>?<VB.*>+}   # Yardımcı fiil veya sıfat-fiil ve sonuna kadar olan fiillerden oluşan bir VP
    """

# ChunkParser nesnesini oluştur
cp = nltk.RegexpParser(grammar)

# Chunking işlemi için metnin etiketlenmiş kelimelerini kullanarak ağaçları oluştur
tree = cp.parse(tagged_tokens)

# Oluşturulan ağacı ekrana yazdır
print(tree)
~~~~
 

~~~~
(S
  I/PRP
  (VP have/VBP)
  (NP a/DT dog/NN)
  (VP named/VBN)
  Max/NNP
  
  ./.
  
  He/PRP
  (VP is/VBZ)
  a/DT
  black/JJ
  Labrador/NNP
  Retriever/NNP
  
  ./.
  
  Max/NNP
  (VP loves/VBZ)
  to/TO
  (VP play/VB)
  (NP fetch/NN)
  with/IN
  his/PRP$
  (NP tennis/NN)
  (NP ball/NN)
  ./.)
~~~~

Grammar değişkeni, yukarıda bahsettiğimiz dil bilgisi kurallarının (grammar rules) tanımlandığı bir yapıdır. Bu yapı, dilin yapısını ve sözdizimini belirleyen kuralların bir listesini içerir. grammar değişkeninde kullanılan kurallar, sözcüklerin ve sözcük gruplarının nasıl bir araya gelebileceğini belirler ve bu sayede dil işleme (NLP) işlemlerinde kullanılır.

Örneğin, grammar değişkenindeki ifade 

    NP: {<DT>?<JJ>*<NN>*}

Bu regular expression (düzenli ifade), NP (isim öbeği) olarak etiketlenen yapıları yakalamak için kullanılmaktadır.

Bu düzenli ifade, "DT" (belirteç) etiketi, "JJ" (sıfat) etiketi ve "NN" (isim) etiketi içeren kelimeleri yakalamak için bir desen belirler. "?" sembolü, "DT" etiketinin var olabileceğini veya olmayabileceğini ifade eder. "\*" sembolü, "JJ" veya "NN" etiketlerinin sıfır veya daha fazla kez tekrarlanabileceğini ifade eder.

Böylece, NP etiketini taşıyan bir yapıda belirteç olabilir veya olmayabilir, ardından sıfır veya daha fazla sıfat, ardından sıfır veya daha fazla isim gelebilir. Örneğin "the big red ball" ifadesi, NP etiketiyle etiketlenecektir çünkü "the" belirteci, "big" ve "red" sıfatları ve "ball" ismi içerir ve bu düzenli ifade tarafından yakalanacaktır.


## Named entity recognition















