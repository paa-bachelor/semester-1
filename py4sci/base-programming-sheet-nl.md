# Base Programming Sheet(NL)

**[Strings]**

str1.split('x') geeft een lijst terug met de string gesplitst op elke x

str1.strip('x') haalt x weg (voor en achteraan de string)
  -> str1.lstrip('x') haalt vooraan de string weg
  -> str1.rstrip('x') haalt achteraan de string weg

str1.isalpha() geeft True als elk element uit str1 in het alfabet zit

str1.replace(str2,'x') vervangt str2 in str1 door x

str1.zfill(x) str1 wordt vooraan aangevuld met 0 totdat len = x

str1.index('x') geeft de meest linkse occurence van x in str1

**[List n Tuples]**

list1.append(x) om iets toe te voegen aan een lijst

list1.remove(x) om iets te verwijderen uit de lijst

**[Sort en Sorted]**

list1.sort(key=None, reverse=Bool) verandert de lijst zelf, bij key kan er een functie gespecifieerd worden 
in hoe de list gesorteerd moet worden key=None is default en sorteert alfabetisch, reverse=False(default) 
geeft ascending order
     
sorted(list1,key=None,reverse=Bool) construeert een nieuwe lijst in tegenstolling tot sort
  
'x'.join(list1) converteert elk element uit list1 tot een string met 'x' tussen de elementen

-> Sets n Dictionaries

dict1[obj1] = obj2

set1 = {A,B} , set2 = {B,C}

set1.pop() geeft een willekeurig element van de set en verwijderd deze uit de set

set1 & set2 = {B} gemeenschappelijke elementen

set1 | set2 = {A,B,C} unie

set1 - set2 = {A,B} verschil van gemeenschappelijke elementen, assymetrisch

sets iteraten door list(set1)
	

**[Tekstbestanden]**

obj.read(x) weergeeft het bestand als string tot het x'ste element, default is volledige file

->(kan gebruikt worden in een while loop: while obj.read(x): , wanneer deze module geen output meer heeft, of het einde van de 
file heeft bereikt, gaat hij een False bool teruggeven en de while loop stoppen.)
            
obj.seek(x) cursor wederkeert naar positie x

obj.tell() weergeeft de positie van de cursor

obj.readline() weergeeft de line waarop de cursor staat als string (tot na de \n dus)

obj.readlines() weergeeft de hele file als een lijst van strings met elke string zijnde een lijn

iter(obj) itereert over de file, next(iter(obj)) geeft dan elke lijn als string:

          for regel in open('file.txt'):
              print(regel)
  waarbij er dus geiterate wordt over de file met regel de iterator

**[Datetime module]**

	import datetime
date1.timetuple() geeft extra tijdinfo
    -> zo geeft tm_yday de dag van het jaar, date1.timetuple().tm_yday


**[Errors]**

	assert a==b,'errormsg'
	raise ValueError('errormsg')


**[Misc.]**

print(obj, end='x') print kan een tweede argument gegeven worden waarbij er dan gestopt wordt op het moment dat er 'x'
voorkomt in de regel

type(obj) weergeeft de type van het object(string, list, tuple...) of obj.__class__ is identiek

obj:.xf met x een int en obj een float, weergeeft obj tot en met x cijfers na de komma

random module reeks 7 tips

isinstance(obj1,type) geeft true voor als obj1 van type type is

zip(seq1,seq2)
 -> iterate over beide seq1 en seq2 dus als i, [(seq1[0],seq2[0]),...,(seq1[i],seq2[i])]
