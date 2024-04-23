Reporte de Consultas en Prolog <br> 

En este reporte se detallan las consultas realizadas sobre una base de conocimiento en Prolog que describe relaciones familiares. Se han utilizado reglas para determinar diferentes tipos de parentesco, como padres, abuelos, hermanos, tías, tíos y ancestros. Además, se han propuesto y probado tres reglas adicionales para determinar si una persona es hermana/o, hermana/o mayor o hermana/o menor de otra persona.<br> 

Base de Conocimiento<br> 

/* Facts*/<br> 
male(jack).<br> 
male(oliver).<br> 
male(ali).<br> 
male(james).<br> 
male(simon).<br> 
male(harry).<br> 
female(helen).<br> 
female(sophie).<br> 
female(jess).<br> 
female(lily).<br> 

parent_of(jack,jess).<br> 
parent_of(jack,lily).<br> 
parent_of(helen, jess).<br> 
parent_of(helen, lily).<br> 
parent_of(oliver,james).<br> 
parent_of(sophie, james).<br> 
parent_of(jess, simon).<br> 
parent_of(ali, simon).<br> 
parent_of(lily, harry).<br> 
parent_of(james, harry).<br> 

/* Reglas */<br> 
father_of(X,Y):- male(X),<br> 
    parent_of(X,Y).<br> 

mother_of(X,Y):- female(X),<br> 
    parent_of(X,Y).<br> 

grandfather_of(X,Y):- male(X),<br> 
    parent_of(X,Z),<br> 
    parent_of(Z,Y).<br> 

grandmother_of(X,Y):- female(X),<br> 
    parent_of(X,Z),<br> 
    parent_of(Z,Y).<br> 

sister_of(X,Y):- female(X),<br> 
    parent_of(F, Y), parent_of(F,X),X \= Y.<br> 

aunt_of(X,Y):- female(X),<br> 
    parent_of(Z,Y), sister_of(Z,X),!.<br> 

brother_of(X,Y):- male(X),<br> 
    parent_of(F, Y), parent_of(F,X),X \= Y.<br> 

uncle_of(X,Y):-<br> 
    parent_of(Z,Y), brother_of(Z,X).<br> 

ancestor_of(X,Y):- parent_of(X,Y).<br> 
ancestor_of(X,Y):- parent_of(X,Z),<br> 
    ancestor_of(Z,Y).<br> 

/* Reglas adicionales */<br> 
sibling_of(X,Y):- parent_of(P, X), parent_of(P, Y), X \= Y.<br> 

older_sibling_of(X,Y):- sibling_of(X,Y), male(X), parent_of(P,X), parent_of(P,Y), X \= Y.<br> 

younger_sibling_of(X,Y):- sibling_of(X,Y), male(Y), parent_of(P,X), parent_of(P,Y), X \= Y.<br> 

Consultas Realizadas<br> 

Consulta: Determinar si Jack es el padre de Jess y Lily.<br> 
father_of(jack, jess).<br> 
father_of(jack, lily).<br> 

Consulta: Determinar quiénes son los abuelos paternos y maternos de Simon.<br> 
grandfather_of(X, simon).<br> 
grandmother_of(X, simon).<br> 

Consulta: Determinar quiénes son las hermanas de James.<br> 
sister_of(X, james).<br> 

Consulta: Determinar quiénes son las tías de Harry.<br> 
aunt_of(X, harry).<br> 

Consulta: Determinar quiénes son los tíos de Harry.<br> 
uncle_of(X, harry).<br> 

Consulta: Determinar los ancestros de Harry.<br> 
ancestor_of(X, harry).<br> 

Consulta: Determinar quiénes son los hermanos de Simon.<br> 
sibling_of(X, simon).<br> 

Consulta: Determinar quiénes son los hermanos mayores de Simon.<br> 
older_sibling_of(X, simon).<br> 

Consulta: Determinar quiénes son los hermanos menores de Simon.<br> 
younger_sibling_of(X, simon).<br> 

Conclusiones<br> 

En este ejercicio, se ha utilizado Prolog para modelar relaciones familiares y determinar diferentes tipos de parentesco entre individuos. Las reglas definidas han permitido responder a consultas sobre padres, abuelos, hermanos, tíos, tías y ancestros. Además, se han propuesto y probado reglas adicionales para determinar si una persona es hermana/o, hermana/o mayor o hermana/o menor de otra persona. Estas reglas han demostrado ser útiles para el análisis de relaciones familiares en un contexto lógico y programático.<br> 
