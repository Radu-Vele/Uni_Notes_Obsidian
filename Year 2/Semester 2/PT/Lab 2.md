---
tags: [Notebooks/PT]
title: Lab 2
created: '2022-03-02T16:08:29.725Z'
modified: '2022-03-02T16:13:05.604Z'
---

# Lab 2

## GUI Example

	- impartire interfata grafica in diferite feluri
	- structurare front-end pe Swing in exemplele din proiect
	- Ex1: view si controller in aceeasi clasa (daca nu avem multe butoane)
	- Ex2: alta implementare pe action Listener (ugly code)
	- Ex3: Controller class: - se preia view ul in care e declarat controller ul, sunt performed stuff din view
		View class: frame - se instantiaza un controller, la buton se adauga add action listener de controller
	
	- Ex4: la fiecare buton este controller ul lui (MY_CHOICE)


## Class diagrams Theory bubble:

	 *A apare instanta de clasa B
		- association: A contine camp de B 
		- aggregation: in A e o colectie de B (Lista, nu atribute separate)
		- composition: agregare in care nu poate exista A fara B (our case) (romb plin - polinom cu monoame)
		- dependency: alte cazuri in care B e in A fara sa fie camp (variabila locala, camp static...)
	
	 *B este parent
		- inheritance (class A extends b)
		- implementation


## MVC: used in WebApps a lot

	- Model - ar trebui sa fie o clasa de string in our case Ex3 sau Ex4 
	- View - interfata CLayout (in cazul nostru nu stie de polinom, deci polinom/monom nu e in model)
	- Controller - metode cand apasam butoane


## In our case:

- View - implementeaza JFrame

- Controller - implementeaza action listeners (-----|>)

- Clasa operatii - depinde de polinom (dependency) - ex: public Polinom add(Pa, Pb);

- Clase: polinom monom care nu e in view



Unde salvam polinoamele citite? (Variabile de stare) -> pot fi tinute in controller (opperand1, opperand2)


* Add method de refresh UI in care sa afisam rezultatul (optional)



Polinom (primeste un string in constructor (RegEx) si genereaza o lista de monoame)

	Pattern: regular expression
		- pentru minus tratam +-, facem split dupa plus
	Generam lista de monoame (foreach)


CCR: 
	- Split regular expression (metoda in polinom string to monomial list);



## Solution RegEx handling:


string format: "2.0\*x\^1+2\*x\^2"

1. Search for the pattern in the input string - done
	1.1. Check if the pattern is found(assemble groups?) -done
2. Save the obtained groups: ex 2.4*x^2+ - in an ArrayList

3. Extract the components (regex?): coefficient Double.parseDouble(2.4) index = Integer.parseInt(2)
take string 2.2*x^1 -> the coefficient is followed by a * "\d.\d[*]" - select the found string -> parse to double
							-> index follows a ^ "[\^]\d" - select the found string -> parse to Int

4. Create monomial, append to monomialList;
