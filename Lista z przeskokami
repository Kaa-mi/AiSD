import random as rd
rd.seed()


#TWORZĘ WĘZŁY:
class Nenufar: #węzły
  def __init__(self,wartosc,poziom):
    self.w=wartosc
    self.wsk=[None]*poziom

  def wysokosc(self):
    wys=0
    for i in self.wsk:
        wys+=1
    return wys
  
  def set_wsk(self,wart):
    for i in range(len(self.wsk)):
      if wart[i]:
        self.wsk[i]=wart[i]
      

#pomocnik przy wyswietlaniu, ktory tworzy kopie Nenufara, przy czym kazda kopia ma poziom glowy,ale zapaleniony wskaznikami tylko do swojej wysokosci,a reszta to None
class Kopia:
  def __init__(self,maxpoziom):
    self.wsk=[None]*maxpoziom

  def kalka(self,Nenufar):
    for i in range(len(Nenufar.wsk)):
      if Nenufar.wsk[i]:
       self.wsk[i]=Nenufar.wsk[i]


#LISTA Z PRZESKOKAMI
class WyscigZab:

  #GŁOWA JEST POZA WSZLEKIMI DZIAŁANIAMI W LIŚCIE,DLATEGO JEJ WARTOŚĆ NIE JEST ISTOTNA
  def __init__(self,wartosc=0,maxpoziom=4): #glowa domyslnie ma wartosc 0,a max poziom wezlow to 4# sprawdzone dla roznych poziomow dziala :D:D:D
    self.poziom=maxpoziom
    self.head=Nenufar(wartosc,maxpoziom)#
    
  #LOSOWO USTAWIA POZIOM DODAWANEGO WEZLA
  def ustaw_wys(self):     #losuje poziom nowego wezla
    wys=rd.randint(1,self.poziom)
    return wys

  #AKTUALIZUJE STAN POWIĄZAŃ W LIŚCIE
  def aktualizuj(self,newN,nextN=None):
    current=self.head 
    while(current!=newN):#inaczej dopisze jeszcze do newN
      wysN=newN.wysokosc()
      wysC=current.wysokosc()
      if wysN<=wysC:
        wysokosc=wysN
      else:
        wysokosc=wysC
      for i in reversed(range(wysokosc)): 
        if current.wsk[i]==None:
          current.wsk[i]=newN #wszystko to co jest puste i w wysokosci newN podczepi pod new  
        elif current.wsk[i]==nextN:
          current.wsk[i]=newN
          newN.wsk[i]=nextN
        elif current.wsk[i].w>newN.w:#cos pokazuje ,ale to nie jest nextN i to coś ma wieksza wartosc niz newN
          tmp=current.wsk[i]
          current.wsk[i]=newN
          newN.wsk[i]=tmp
      current=current.wsk[0] 

  #ODCINA NODA DO USUNIĘCIA 
  def dezaktywacja(self,delN):
    current=self.head
    while(current): #przeszukuje calą listę, wyszykując wszstkie Nenufary, które wskazują na ten do usunięcia
      wysD=delN.wysokosc()
      wysC=current.wysokosc()
      if wysD<=wysC:
        wysokosc=wysD
      else:
        wysokosc=wysC
      for i in reversed(range(wysokosc)): 
        if current.wsk[i]==delN: #jeśli któryś z wskażników pokazuje na usuwany Nenufar, to go zeruje
          current.wsk[i]=None #zerowanie dotyczy też wsk[0], co spr, że lista doleci tylko do Nnufara przed tym, który usuwamy i nie będzie bez potrzeby spr kolejnych.
      current=current.wsk[0] 

  #DODAJE NOWEGO NODA (nie można dodać nowej glow, ona jest nietykalna :D)
  def dodaj(self,wartosc): 
    poziomN=self.ustaw_wys() #ustawia lososo poziom nowego Nenufara
    print('poziom wezla',poziomN)
    newN=Nenufar(wartosc,poziomN)
    nextN=self.poskaczmy(wartosc).wsk[0]
  
    self.aktualizuj(newN,nextN) #już dowiąże noda i zaktualizuje resztę

  #ZDNAJDUJE ODPOWIEDNIEGO NENUFARA
  def poskaczmy(self,el,zaw=0): #zaw argument potrzeby do moich celow ;) w metodzie ZAWODY
    current=self.head 
    i=self.poziom-1 
    skoki=0
    while(True):
      skoki+=1
      if current.wsk[i]==None or current.wsk[i].w>el: #jezeli dany wskaznik pokazuje na null, to schodzim pietro nizej w danym nodzie
        i-=1 #zmniejszamy indeks
      elif current.wsk[i].w<el: #wskaznik pokazuje na cos i element jest wiekszy niz wartos tego czegos, zmieniamy wiec current
        current=current.wsk[i]  
      elif current.wsk[i].w==el:
        current=current.wsk[i]
        break
      if i<0:
        break
    
    if zaw==1:
      return skoki
    else:
      return current
    #jesli nie znjdzie el w liscie,to zwroci wartosc najblizszej mniejszej :)

  #TAKIE TAM MOJE ZABAWY ;) SPRAWDZAJĄCE NA ILE TA METODA JEST SKUTECZNA ;)
  def zawody(self,el):
      prosto=0
      currNode=self.head
      while(currNode): #Zaba skacze prosto
        if currNode.w==el:
          break
        currNode=currNode.wsk[0]
        prosto+=1
      skoki=self.poskaczmy(el,1)
      
      print('\nAMBITNA ŻABA SKOCZYŁA',skoki,'RAZY NA NENUFAR NR',el,'I ',end='')
      if prosto>skoki:
        print('WYGRAŁA :) Z ŻABĄ SKACZĄCĄ PROSTO, KTÓRA SKOCZYŁA',prosto,'RAZY.')
      elif prosto==skoki:
        print('ZREMISOWAŁA Z ŻABĄ SKACZĄCĄ PROSTO, KTÓRA SKOCZYŁA',prosto,'RAZY.')
      elif prosto<skoki:
        print('MOGŁA SKAKAĆ PROSTĄ DROGĄ,BO ŻABA SKACZĄCĄ PROSTO,SKOCZYŁA TYLKO',prosto,'RAZY.')

  #USUWANIE DOWOLNEGO NENUFARA Z LISTY
  def byebye(self,el):
    prevN=self.poskaczmy(el-1)
    delN=self.poskaczmy(el) 
    nextN=delN.wsk[0]
    if prevN != delN: #zabezpieczenie w przpadku,gdy podanego elementu nie będzie na liście
      self.dezaktywacja(delN)
      while(nextN): #trzeba aktualizowac dla wszystkich pozostalych wezlow
        self.aktualizuj(nextN)
        nextN=nextN.wsk[0]
    else:
      print('WARTOŚCI NIE MA W LIŚCIE')

  #ZLICZA DŁUGOŚĆ CAŁEJ LISTY
  def ilosc_wezlow(self):
    licznik=0
    currNode=self.head
    while(currNode):
      licznik+=1
      currNode=currNode.wsk[0]
    return licznik

  #STWORZONE TYLKO NA POTRZEBY WYŚWIETLANIA
  #TWORZ KOPIĘ LISTY,ALE TAKĄ, KTÓREJ WSZYSTKIE WĘZŁY MAJĄ TEN SAM POZIOM
  def tworz_kopie(self,dl_listy):
    Kopie=[]
    current=self.head
    for j in range(dl_listy):  #Tworze kopie Nenufara
      kopia=Kopia(self.poziom)
      kopia.kalka(current)
      Kopie.append(kopia)
      current=current.wsk[0]
    return Kopie

  #WYŚWIETLANIE LISTY WRAZ Z WSZYSTKIMI POWIĄZANANIAMI
  def wyswietl(self): #no to zaczynam zabawe :/ 
    print('\n\t\t AKTUALNY ROZKLAD NENUFARÓW NA JEZIORZE\n')
    dl_listy=self.ilosc_wezlow()
    Kopie=self.tworz_kopie(dl_listy-1) 
    
    for i in reversed(range(self.poziom)):
      current=Kopie[0]
      nextN=current.wsk[0]
      counter=0
      while(counter < (dl_listy-1)): #czyli poki mamy jakiegos nexta
        if counter==0:
          print('  o  ',end='')

        if current.wsk[i]!=nextN:
          print('------',end='')
        elif current.wsk[i]==nextN:
          print('--> o ',end='')
          current=nextN
        
        counter+=1
        if counter < (dl_listy-1):
          nextN=Kopie[counter].wsk[0]
      
      print('--> NULL ',end='')
      print()
    print('HEAD',end=' ')
    last=self.head.wsk[0]
    while(last):
      if last.w>9 or last.w<0: #mala kosmetyka
        print('  ',last.w,'',end='')
      else:
        print('   ',last.w,'',end='')
      last=last.wsk[0]
   
    print()
  
  #DZIALA :D:D:D Sprawdone dla roznych ilosci wezlow i roznych wysokosci.



skoki=WyscigZab() 

print('\nDodaję Nenufar o wartości 1:')
skoki.dodaj(1)
print('\nDodaję Nenufar o wartości 2:')
skoki.dodaj(2)
print('\nDodaję Nenufar o wartości 3:')
skoki.dodaj(3)
print('\nDodaję Nenufar o wartości 4:')
skoki.dodaj(4)
print('\nDodaję Nenufar o wartości 5:')
skoki.dodaj(5)
print('\nDodaję Nenufarr o wartości 7:')
skoki.dodaj(7)
print('\nDodaję Nenufarr o wartości 10:')
skoki.dodaj(10)
print('\nDodaję Nenufar o wartości 11:')
skoki.dodaj(11)
print('\nDodaję Nenufar o wartości 8:')
skoki.dodaj(8)
print('\nDodaję Nenufar o wartości 9:')
skoki.dodaj(9)

skoki.wyswietl()
print()

print('\nTeraz trzebaby trochę pousuwać:')
print('Bye bye 8')
skoki.byebye(8)
#skoki.wyswietl()
print('Bye bye 1')
skoki.byebye(1)
skoki.wyswietl()
print('\nTeraz znów dodaję, teraz 21:')
skoki.dodaj(21)
#skoki.wyswietl()

print('\nTeraz sprawdzam czy dodawanie zadziała dla wartości minusowych')
skoki.dodaj(-1)
skoki.wyswietl()
print('\nDZIAŁA')

print('\nCo jak będę chciała usunąć wartość, której nie ma?')
skoki.byebye(20)
skoki.wyswietl()
print('\nDZIAŁA')

print('\nA co jak będę chciała usunąć głowę?')
skoki.byebye(0)
skoki.wyswietl()
print('\nDZIAŁA. Nie stracę głowy :)')

print('Sprawdzam czy to faktycznie dziala')
skoki.zawody(4)
skoki.zawody(-1)
skoki.zawody(10)

